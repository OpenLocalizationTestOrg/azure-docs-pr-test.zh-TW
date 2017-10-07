---
title: "aaaView 及管理 StorSimple Virtual Array 工作 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員服務工作 頁面以及 toouse 它的 hello StorSimple Virtual Array 的 tootrack 最近和目前工作。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="e46b1-103">用於 hello StorSimple Virtual Array hello StorSimple 裝置管理員服務 tooview 工作</span><span class="sxs-lookup"><span data-stu-id="e46b1-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="e46b1-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e46b1-104">Overview</span></span>
<span data-ttu-id="e46b1-105">hello**作業**刀鋒視窗提供單一中央入口網站，以檢視及管理連線的 tooyour StorSimple 裝置管理員服務的虛擬陣列已啟動的工作。</span><span class="sxs-lookup"><span data-stu-id="e46b1-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="e46b1-106">您可以針對多個虛擬裝置，檢視執行中、完成和失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="e46b1-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="e46b1-107">結果會以表格式格式呈現。</span><span class="sxs-lookup"><span data-stu-id="e46b1-107">Results are presented in a tabular format.</span></span>

![[作業] 刀鋒視窗](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="e46b1-109">您可以快速尋找您感興趣的這類的欄位進行篩選的 hello 工作：</span><span class="sxs-lookup"><span data-stu-id="e46b1-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="e46b1-110">**時間範圍**– 工作可以篩選根據的 hello 日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e46b1-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="e46b1-111">**裝置**– 連接的特定裝置 tooyour 服務上起始工作。</span><span class="sxs-lookup"><span data-stu-id="e46b1-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="e46b1-112">hello 已篩選的工作會再製成資料表根據 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="e46b1-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="e46b1-113">**名稱**– hello 工作名稱可以是**所有**，**備份**，**複製**，**容錯移轉**，**下載更新**，或**安裝更新**。</span><span class="sxs-lookup"><span data-stu-id="e46b1-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="e46b1-114">**狀態** – 作業可以是 [全部]、[進行中]、[成功]、[失敗]或 [已取消]。</span><span class="sxs-lookup"><span data-stu-id="e46b1-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="e46b1-115">**實體**– hello 工作可以與磁碟區、 共用或裝置產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e46b1-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="e46b1-116">**裝置**– hello hello 裝置的 hello 已啟動工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="e46b1-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="e46b1-117">**在啟動**– hello hello 作業啟動時的時間。</span><span class="sxs-lookup"><span data-stu-id="e46b1-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="e46b1-118">**持續時間**– hello 執行 hello 作業的持續時間。</span><span class="sxs-lookup"><span data-stu-id="e46b1-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="e46b1-119">**狀態** – 您可以搜尋全部、執行中、完成或已取消的作業。</span><span class="sxs-lookup"><span data-stu-id="e46b1-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="e46b1-120">**作業類型**– hello 作業類型可為 all、 備份、 還原容錯移轉、 下載更新，或安裝更新。</span><span class="sxs-lookup"><span data-stu-id="e46b1-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="e46b1-121">hello 工作清單會重新整理每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="e46b1-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="e46b1-122">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="e46b1-122">View job details</span></span>
<span data-ttu-id="e46b1-123">執行下列步驟 tooview hello 詳細資料的任何作業的 hello。</span><span class="sxs-lookup"><span data-stu-id="e46b1-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="e46b1-124">tooview 工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="e46b1-124">tooview job details</span></span>
1. <span data-ttu-id="e46b1-125">在 hello**作業**刀鋒視窗，顯示 hello 工作，您有興趣使用適當的篩選器執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e46b1-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="e46b1-126">您可以搜尋完成或執行中作業。</span><span class="sxs-lookup"><span data-stu-id="e46b1-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="e46b1-127">從工作 hello 表格式清單中選取工作。</span><span class="sxs-lookup"><span data-stu-id="e46b1-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![[作業] 刀鋒視窗](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="e46b1-129">在 hello hello 頁面底部，按一下**詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="e46b1-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="e46b1-130">在 hello**詳細資料**對話方塊中，您可以檢視狀態、 詳細資料，以及時間統計資料。</span><span class="sxs-lookup"><span data-stu-id="e46b1-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="e46b1-131">hello 如下圖所示的 hello 範例**備份工作詳細資料** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="e46b1-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![工作詳細資料](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="e46b1-133">當 hello 虛擬機器已經暫停 hello hypervisor 中的工作失敗</span><span class="sxs-lookup"><span data-stu-id="e46b1-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="e46b1-134">當工作處於大於 15 分鐘暫停您的 StorSimple Virtual Array 和 hello 裝置 （虛擬機器在 hypervisor 中佈建） 的進度，hello 作業失敗時。</span><span class="sxs-lookup"><span data-stu-id="e46b1-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="e46b1-135">這由於超過 tooyour StorSimple Virtual Array 時間正在與 hello Microsoft Azure 時間同步處理。</span><span class="sxs-lookup"><span data-stu-id="e46b1-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="e46b1-136">您會看到下列錯誤 hello: 「 您的裝置時間是 15 分鐘以上的 hello Microsoft Azure 時間與同步處理。</span><span class="sxs-lookup"><span data-stu-id="e46b1-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="e46b1-137">請確定 hello hypervisor 和 hello 裝置時間與 NTP 伺服器同步。</span><span class="sxs-lookup"><span data-stu-id="e46b1-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="e46b1-138">請確定沒有連線問題。</span><span class="sxs-lookup"><span data-stu-id="e46b1-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="e46b1-139">tootroubleshoot 連線問題，執行診斷測試從 hello 本機 web UI 虛擬裝置。 」</span><span class="sxs-lookup"><span data-stu-id="e46b1-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="e46b1-140">這些失敗會套用 toobackup、 還原、 更新和容錯移轉作業。</span><span class="sxs-lookup"><span data-stu-id="e46b1-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="e46b1-141">如果您的虛擬機器已佈建為 HYPER-V 中，hello 機器最終同步處理時間與您的 hypervisor。</span><span class="sxs-lookup"><span data-stu-id="e46b1-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="e46b1-142">一旦發生這種情況，您可以重新啟動您的作業。</span><span class="sxs-lookup"><span data-stu-id="e46b1-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e46b1-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e46b1-143">Next steps</span></span>
<span data-ttu-id="e46b1-144">[了解如何 toouse 會 hello 本機 web UI tooadminister 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="e46b1-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

