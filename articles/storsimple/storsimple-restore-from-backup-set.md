---
title: "從備份還原 StorSimple 磁碟區 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 的 [備份類別目錄] 頁面，從備份組還原 StorSimple 磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="b2e75-103">從備份組還原 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="b2e75-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="b2e75-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b2e75-104">Overview</span></span>
<span data-ttu-id="b2e75-105">[備份類別目錄]  頁面會顯示在產生手動或自動備份時建立的所有備份組。</span><span class="sxs-lookup"><span data-stu-id="b2e75-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="b2e75-106">您可以使用此頁面來列出備份原則或磁碟區的所有備份、選取或刪除備份，或是使用備份來還原或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![備份類別目錄頁面](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="b2e75-108">本教學課程說明如何使用 [備份資料目錄]  頁面，從備份組還原您裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="b2e75-109">如何使用備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="b2e75-109">How to use the backup catalog</span></span>
<span data-ttu-id="b2e75-110">[備份類別目錄]  頁面提供查詢，可協助您縮小備份組選取範圍。</span><span class="sxs-lookup"><span data-stu-id="b2e75-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="b2e75-111">您可以篩選根據下列參數擷取的備份組：</span><span class="sxs-lookup"><span data-stu-id="b2e75-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="b2e75-112">**裝置** - 建立備份組所在的裝置。</span><span class="sxs-lookup"><span data-stu-id="b2e75-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="b2e75-113">**備份原則**或**磁碟區** – 與此備份組相關聯的備份原則或磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="b2e75-114">**起****迄** – 建立備份組的日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b2e75-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="b2e75-115">接著會根據下列屬性，將篩選的備份組列表顯示：</span><span class="sxs-lookup"><span data-stu-id="b2e75-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="b2e75-116">**名稱** - 與備份組相關聯的備份原則或磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="b2e75-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="b2e75-117">**大小** - 備份組的實際大小。</span><span class="sxs-lookup"><span data-stu-id="b2e75-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="b2e75-118">**建立日期** - 建立備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="b2e75-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="b2e75-119">**類型** - 備份組可以是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="b2e75-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="b2e75-120">本機快照是本機儲存於裝置上的所有磁碟區資料備份，而雲端快照是指位於雲端的磁碟區資料備份。</span><span class="sxs-lookup"><span data-stu-id="b2e75-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="b2e75-121">本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="b2e75-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="b2e75-122">**起始者** - 備份可根據排程自動初始，或由使用者手動初始。</span><span class="sxs-lookup"><span data-stu-id="b2e75-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="b2e75-123">(您可以使用備份原則來排程備份。</span><span class="sxs-lookup"><span data-stu-id="b2e75-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="b2e75-124">或者，可以使用 [取得備份] 選項來取得互動式備份。)</span><span class="sxs-lookup"><span data-stu-id="b2e75-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="b2e75-125">如何從備份還原您的 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="b2e75-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="b2e75-126">您可以使用 [備份類別目錄]  頁面，從特定的備份還原 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="b2e75-127">從備份還原將從備份取代現有的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="b2e75-128">這可能會造成在取得備份之後寫入的所有資料遺失。</span><span class="sxs-lookup"><span data-stu-id="b2e75-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="b2e75-129">在磁碟區上起始還原之前，請確定磁碟區已離線。</span><span class="sxs-lookup"><span data-stu-id="b2e75-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="b2e75-130">您必須先讓主機上的磁碟區離線，再讓裝置離線。</span><span class="sxs-lookup"><span data-stu-id="b2e75-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="b2e75-131">請遵循 [使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="b2e75-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="b2e75-132">執行下列步驟，以從備份組還原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="b2e75-133">從備份組還原</span><span class="sxs-lookup"><span data-stu-id="b2e75-133">To restore from a backup set</span></span>
1. <span data-ttu-id="b2e75-134">在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b2e75-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![備份類別目錄](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="b2e75-136">選取備份組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2e75-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="b2e75-137">選取適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="b2e75-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="b2e75-138">在下拉式清單中，針對要選取的備份選擇磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="b2e75-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="b2e75-139">指定時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b2e75-139">Specify the time range.</span></span>
   4. <span data-ttu-id="b2e75-140">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="b2e75-140">Click the check icon</span></span> ![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="b2e75-142">以執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="b2e75-142">to execute this query.</span></span>
      
      <span data-ttu-id="b2e75-143">與選取的磁碟區或備份原則相關聯的備份應該會出現在備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="b2e75-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="b2e75-144">展開備份組以檢視相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b2e75-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="b2e75-145">您必須先在主機和裝置上將這些磁碟區離線，才能還原它們。</span><span class="sxs-lookup"><span data-stu-id="b2e75-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="b2e75-146">請遵循 [使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="b2e75-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b2e75-147">確定您已先讓主機上的磁碟區離線，然後再讓裝置上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="b2e75-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="b2e75-148">如果您並未讓主機上的磁碟區離線，可能會導致資料損毀。</span><span class="sxs-lookup"><span data-stu-id="b2e75-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="b2e75-149">選取備份組。</span><span class="sxs-lookup"><span data-stu-id="b2e75-149">Select a backup set.</span></span> <span data-ttu-id="b2e75-150">按一下頁面底部的 [還原]  。</span><span class="sxs-lookup"><span data-stu-id="b2e75-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="b2e75-151">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="b2e75-151">You will be prompted for confirmation.</span></span> 
   
    ![確認電子郵件](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="b2e75-153">檢閱還原資訊，然後按一下核取圖示 ![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="b2e75-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="b2e75-154">這將會初始還原工作，而您可以藉由存取 [工作]  頁面來進行檢視。</span><span class="sxs-lookup"><span data-stu-id="b2e75-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="b2e75-155">還原完成之後，您可以確認磁碟區的內容已由備份的磁碟區所取代。</span><span class="sxs-lookup"><span data-stu-id="b2e75-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="b2e75-156">![提供的影片](./media/storsimple-restore-from-backup-set/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="b2e75-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="b2e75-157">若要觀看影片示範如何使用 StorSimple 的複製和還原功能，將已刪除的檔案復原，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="b2e75-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e75-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2e75-158">Next steps</span></span>
* <span data-ttu-id="b2e75-159">了解如何 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="b2e75-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="b2e75-160">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="b2e75-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

