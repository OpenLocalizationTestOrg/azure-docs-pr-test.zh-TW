---
title: "Microsoft Azure StorSimple Virtual Array 備份教學課程 | Microsoft Docs"
description: "說明如何備份 StorSimple Virtual Array 共用與磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="f082f-103">備份 StorSimple Virtual Array 上的共用或磁碟區</span><span class="sxs-lookup"><span data-stu-id="f082f-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f082f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f082f-104">Overview</span></span>

<span data-ttu-id="f082f-105">StorSimple Virtual Array 是混合式雲端儲存體內部部署虛擬裝置，可設定為檔案伺服器或 iSCSI 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f082f-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="f082f-106">虛擬陣列可讓使用者為裝置上的所有共用或磁碟區建立排程備份和手動備份。</span><span class="sxs-lookup"><span data-stu-id="f082f-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="f082f-107">設為檔案伺服器時，也可進行項目層級的復原。</span><span class="sxs-lookup"><span data-stu-id="f082f-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="f082f-108">本教學課程說明如何建立排程備份和手動備份，以及執行項目層級復原來還原虛擬陣列上已刪除的檔案。</span><span class="sxs-lookup"><span data-stu-id="f082f-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="f082f-109">本教學課程僅適用於 StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="f082f-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="f082f-110">如需 8000 系列的相關資訊，請參閱[建立 8000 系列裝置的備份](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="f082f-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="f082f-111">備份共用和磁碟區</span><span class="sxs-lookup"><span data-stu-id="f082f-111">Back up shares and volumes</span></span>

<span data-ttu-id="f082f-112">備份可提供共用和磁碟區的時間點保護、改善復原能力，同時讓還原時間降至最低。</span><span class="sxs-lookup"><span data-stu-id="f082f-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="f082f-113">您有兩種方法可以備份 StorSimple 裝置上的共用或磁碟區：「排程」或「手動」。</span><span class="sxs-lookup"><span data-stu-id="f082f-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="f082f-114">下列各節討論上述每一種方法。</span><span class="sxs-lookup"><span data-stu-id="f082f-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="f082f-115">變更備份開始時間</span><span class="sxs-lookup"><span data-stu-id="f082f-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="f082f-116">在此版本中，排程的備份由預設原則建立，該原則會每日在特定時間執行並備份裝置上的所有共用或磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f082f-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="f082f-117">目前無法建立用於排程備份的自訂原則。</span><span class="sxs-lookup"><span data-stu-id="f082f-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="f082f-118">StorSimple Virtual Array 有預設的備份原則會在每日特定時間 (22:30) 啟動，每天備份一次裝置上的所有共用或磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f082f-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="f082f-119">您可以變更備份開始的時間，但無法變更頻率及保留期 (指定備份保留的數量)。</span><span class="sxs-lookup"><span data-stu-id="f082f-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="f082f-120">這些在備份期間會備份整個虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="f082f-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="f082f-121">這可能會對影響裝置的效能和裝置上已部署的工作負載。</span><span class="sxs-lookup"><span data-stu-id="f082f-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="f082f-122">因此，建議您將這些備份排定在離峰時段。</span><span class="sxs-lookup"><span data-stu-id="f082f-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="f082f-123">若要變更預設的備份開始時間，請在 [Azure 入口網站](https://portal.azure.com/)中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f082f-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="f082f-124">變更預設備份原則的開始時間</span><span class="sxs-lookup"><span data-stu-id="f082f-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="f082f-125">移至 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="f082f-125">Go to **Devices**.</span></span> <span data-ttu-id="f082f-126">將會顯示已向您的 StorSimple 裝置管理員服務註冊的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="f082f-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![瀏覽至裝置](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="f082f-128">選取並按一下您的裝置。</span><span class="sxs-lookup"><span data-stu-id="f082f-128">Select and click your device.</span></span> <span data-ttu-id="f082f-129">[設定] 刀鋒視窗隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f082f-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="f082f-130">移至 [管理] > [備份原則]。</span><span class="sxs-lookup"><span data-stu-id="f082f-130">Go to **Manage > Backup policies**.</span></span>
   
    ![選取您的裝置](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="f082f-132">在 [備份原則] 刀鋒視窗中，預設開始時間為 22:30。</span><span class="sxs-lookup"><span data-stu-id="f082f-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="f082f-133">您可以在裝置時區中為每日排程指定新的開始時間。</span><span class="sxs-lookup"><span data-stu-id="f082f-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![瀏覽至備份原則](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="f082f-135">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="f082f-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="f082f-136">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="f082f-136">Take a manual backup</span></span>

<span data-ttu-id="f082f-137">除了排程備份，您隨時可以手動 (依需要) 備份裝置資料。</span><span class="sxs-lookup"><span data-stu-id="f082f-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="f082f-138">建立手動備份</span><span class="sxs-lookup"><span data-stu-id="f082f-138">To create a manual backup</span></span>

1. <span data-ttu-id="f082f-139">移至 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="f082f-139">Go to **Devices**.</span></span> <span data-ttu-id="f082f-140">選取您的裝置，然後以滑鼠右鍵按一下選取的資料列中最右邊的 [...]。</span><span class="sxs-lookup"><span data-stu-id="f082f-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="f082f-141">從操作能表中，選取 [進行備份]。</span><span class="sxs-lookup"><span data-stu-id="f082f-141">From the context menu, select **Take backup**.</span></span>
   
    ![瀏覽至進行備份](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="f082f-143">在 [進行備份] 刀鋒視窗中，按一下 [進行備份]。</span><span class="sxs-lookup"><span data-stu-id="f082f-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="f082f-144">這樣會備份檔案伺服器上的所有共用，或 iSCSI 伺服器上的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="f082f-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![正在啟動備份](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="f082f-146">依需求備份開始執行，您會看到備份作業已啟動。</span><span class="sxs-lookup"><span data-stu-id="f082f-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![正在啟動備份](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="f082f-148">作業順利完成後會再次通知您。</span><span class="sxs-lookup"><span data-stu-id="f082f-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="f082f-149">備份程序接著開始。</span><span class="sxs-lookup"><span data-stu-id="f082f-149">The backup process then starts.</span></span>
   
    ![已建立備份工作](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="f082f-151">若要追蹤備份進度和查看作業詳細資料，請按一下通知。</span><span class="sxs-lookup"><span data-stu-id="f082f-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="f082f-152">這會帶您前往 [作業詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="f082f-152">This takes you to  **Job details**.</span></span>
   
     ![備份作業詳細資料](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="f082f-154">備份完成後，請移至 [管理] > [備份目錄]。</span><span class="sxs-lookup"><span data-stu-id="f082f-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="f082f-155">您會看到裝置上所有共用 (或磁碟區) 的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="f082f-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![已完成的備份](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="f082f-157">檢視現有的備份</span><span class="sxs-lookup"><span data-stu-id="f082f-157">View existing backups</span></span>
<span data-ttu-id="f082f-158">若要檢視現有備份，請在 Azure 入口網站中執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f082f-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="f082f-159">檢視現有備份</span><span class="sxs-lookup"><span data-stu-id="f082f-159">To view existing backups</span></span>

1. <span data-ttu-id="f082f-160">移至 [裝置] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f082f-160">Go to **Devices** blade.</span></span> <span data-ttu-id="f082f-161">選取並按一下您的裝置。</span><span class="sxs-lookup"><span data-stu-id="f082f-161">Select and click your device.</span></span> <span data-ttu-id="f082f-162">在 [設定] 刀鋒視窗中，移至 [管理] > [備份目錄]。</span><span class="sxs-lookup"><span data-stu-id="f082f-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![瀏覽至備份目錄](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="f082f-164">指定下列準則以用於篩選︰</span><span class="sxs-lookup"><span data-stu-id="f082f-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="f082f-165">**時間範圍** – 可以是 [過去 1 小時]、[過去 24 小時]、[過去 7 天]、[過去 30 天]、[過去一年] 和 [自訂日期]。</span><span class="sxs-lookup"><span data-stu-id="f082f-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="f082f-166">**裝置** – 從已向 StorSimple 裝置管理員服務註冊的檔案伺服器或 iSCSI 伺服器清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="f082f-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="f082f-167">**已起始** – 可以自動地 [已排程] \(依備份原則) 或 [手動] 起始 (由您執行)。</span><span class="sxs-lookup"><span data-stu-id="f082f-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![篩選備份](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="f082f-169">按一下 [Apply (套用)] 。</span><span class="sxs-lookup"><span data-stu-id="f082f-169">Click **Apply**.</span></span> <span data-ttu-id="f082f-170">已篩選的備份清單會顯示在 [備份目錄] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="f082f-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="f082f-171">請注意，永遠只會顯示 100 個備份項目。</span><span class="sxs-lookup"><span data-stu-id="f082f-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![更新備份目錄](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="f082f-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f082f-173">Next steps</span></span>

<span data-ttu-id="f082f-174">深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="f082f-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

