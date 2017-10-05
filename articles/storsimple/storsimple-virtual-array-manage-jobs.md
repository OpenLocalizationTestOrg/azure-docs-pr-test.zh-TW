---
title: "檢視和管理 StorSimple Virtual Array 作業 | Microsoft Docs"
description: "說明 StorSimple 裝置管理員服務的「作業」頁面，以及如何使用該頁面來追蹤 StorSimple Virtual Array 的最近和目前作業。"
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="7572b-103">使用 StorSimple 裝置管理員服務來檢視 StorSimple Virtual Array 的作業</span><span class="sxs-lookup"><span data-stu-id="7572b-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="7572b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7572b-104">Overview</span></span>
<span data-ttu-id="7572b-105">[作業] 刀鋒視窗提供單一中央入口網站，可檢視和管理已連接至 StorSimple 裝置管理員服務的虛擬陣列上啟動的作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="7572b-106">您可以針對多個虛擬裝置，檢視執行中、完成和失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="7572b-107">結果會以表格式格式呈現。</span><span class="sxs-lookup"><span data-stu-id="7572b-107">Results are presented in a tabular format.</span></span>

![[作業] 刀鋒視窗](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="7572b-109">您可以透過篩選欄位，快速找到您所感興趣的工作，例如：</span><span class="sxs-lookup"><span data-stu-id="7572b-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="7572b-110">**時間範圍** – 您可以根據日期和時間範圍來篩選作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="7572b-111">**裝置** – 作業會在連線到服務的特定裝置上進行初始化。</span><span class="sxs-lookup"><span data-stu-id="7572b-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="7572b-112">接著會根據下列屬性，將篩選的作業列表顯示：</span><span class="sxs-lookup"><span data-stu-id="7572b-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="7572b-113">**類型** – 作業名稱可以是 [全部]、[備份]、[還原]、[容錯移轉]、[下載更新]，或 [安裝更新]。</span><span class="sxs-lookup"><span data-stu-id="7572b-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="7572b-114">**狀態** – 作業可以是 [全部]、[進行中]、[成功]、[失敗]或 [已取消]。</span><span class="sxs-lookup"><span data-stu-id="7572b-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="7572b-115">**實體** – 作業可以與磁碟區、共用或裝置相關聯。</span><span class="sxs-lookup"><span data-stu-id="7572b-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="7572b-116">**裝置** – 用來啟動工作之裝置的名稱。</span><span class="sxs-lookup"><span data-stu-id="7572b-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="7572b-117">**啟動於** – 啟動工作的時間。</span><span class="sxs-lookup"><span data-stu-id="7572b-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="7572b-118">**持續時間** – 作業執行的持續時間。</span><span class="sxs-lookup"><span data-stu-id="7572b-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="7572b-119">**狀態** – 您可以搜尋全部、執行中、完成或已取消的作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="7572b-120">**作業類型** – 作業類型可以是全部、備份、還原、容錯移轉、下載更新或安裝更新。</span><span class="sxs-lookup"><span data-stu-id="7572b-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="7572b-121">工作清單每隔 30 秒會重新整理。</span><span class="sxs-lookup"><span data-stu-id="7572b-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="7572b-122">檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="7572b-122">View job details</span></span>
<span data-ttu-id="7572b-123">執行下列步驟來檢視任何工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7572b-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="7572b-124">若要檢視工作詳細資料</span><span class="sxs-lookup"><span data-stu-id="7572b-124">To view job details</span></span>
1. <span data-ttu-id="7572b-125">在 [作業] 刀鋒視窗上，搭配適當的篩選執行查詢，以顯示您感興趣的作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="7572b-126">您可以搜尋完成或執行中作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="7572b-127">從作業表格式清單中選取作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-127">Select a job from the tabular list of jobs.</span></span>
   
    ![[作業] 刀鋒視窗](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="7572b-129">按一下頁面底部的 [詳細資料] 。</span><span class="sxs-lookup"><span data-stu-id="7572b-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="7572b-130">在 [詳細資料]  對話方塊中，您可以檢視狀態、詳細資料和時間統計資料。</span><span class="sxs-lookup"><span data-stu-id="7572b-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="7572b-131">下圖顯示 [備份作業詳細資料]  對話方塊的範例。</span><span class="sxs-lookup"><span data-stu-id="7572b-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![工作詳細資料](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="7572b-133">虛擬機器在 hypervisor 中暫停時，作業失敗</span><span class="sxs-lookup"><span data-stu-id="7572b-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="7572b-134">當 StorSimple Virtual Array 上正在執行作業且裝置 (Hypervisor 中佈建的虛擬機器) 暫停超過 15 分鐘時，作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="7572b-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="7572b-135">這是因為您的 StorSimple Virtual Array 時間未與 Microsoft Azure 時間同步處理。</span><span class="sxs-lookup"><span data-stu-id="7572b-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="7572b-136">您會看到下列錯誤：「您的裝置時間與 Microsoft Azure 不同步超過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="7572b-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="7572b-137">請確定 Hypervisor 和裝置時間與 NTP 伺服器同步。</span><span class="sxs-lookup"><span data-stu-id="7572b-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="7572b-138">請確定沒有連線問題。</span><span class="sxs-lookup"><span data-stu-id="7572b-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="7572b-139">若要針對連線問題進行疑難排解，請從虛擬裝置的本機 Web UI 執行診斷測試。」</span><span class="sxs-lookup"><span data-stu-id="7572b-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="7572b-140">備份、還原、更新和容錯移轉作業都可能發生這些失敗。</span><span class="sxs-lookup"><span data-stu-id="7572b-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="7572b-141">如果您的虛擬機器佈建到 Hyper-V，電腦與您的 Hypervisor 時間最終會同步。</span><span class="sxs-lookup"><span data-stu-id="7572b-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="7572b-142">一旦發生這種情況，您可以重新啟動您的作業。</span><span class="sxs-lookup"><span data-stu-id="7572b-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7572b-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7572b-143">Next steps</span></span>
<span data-ttu-id="7572b-144">了解如何[使用本機 Web UI 來管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="7572b-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

