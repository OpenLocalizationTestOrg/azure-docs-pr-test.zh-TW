---
title: "管理您的 StorSimple 備份類別目錄 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 服務的 [備份類別目錄] 頁面列出、選取和刪除磁碟區的備份組。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="dd24e-103">使用 StorSimple Manager 服務管理備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="dd24e-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="dd24e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="dd24e-104">Overview</span></span>
<span data-ttu-id="dd24e-105">StorSimple Manager 服務 [備份類別目錄]  頁面會顯示在進行手動備份或排程備份時所建立的所有備份組。</span><span class="sxs-lookup"><span data-stu-id="dd24e-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="dd24e-106">您可以使用此頁面來列出備份原則或磁碟區的所有備份、選取或刪除備份，或是使用備份來還原或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dd24e-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="dd24e-107">本教學課程說明如何列出、選取和刪除備份組。</span><span class="sxs-lookup"><span data-stu-id="dd24e-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="dd24e-108">若要了解如何透過備份還原裝置內容，請移至 [從備份組還原裝置](storsimple-restore-from-backup-set.md)。</span><span class="sxs-lookup"><span data-stu-id="dd24e-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="dd24e-109">若要了解如何複製磁碟區，請移至 [複製 StorSimple 磁碟區](storsimple-clone-volume.md)。</span><span class="sxs-lookup"><span data-stu-id="dd24e-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![備份類別目錄](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="dd24e-111">[備份類別目錄]  頁面提供查詢，可讓您縮小備份組選取範圍。</span><span class="sxs-lookup"><span data-stu-id="dd24e-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="dd24e-112">您可以篩選根據下列參數擷取的備份組：</span><span class="sxs-lookup"><span data-stu-id="dd24e-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="dd24e-113">**裝置** - 建立備份組所在的裝置。</span><span class="sxs-lookup"><span data-stu-id="dd24e-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="dd24e-114">**備份原則或磁碟區** – 與此備份組相關聯的備份原則或磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dd24e-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="dd24e-115">**起迄** – 建立備份組的日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="dd24e-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="dd24e-116">接著會根據下列屬性，將篩選的備份組列表顯示：</span><span class="sxs-lookup"><span data-stu-id="dd24e-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="dd24e-117">**名稱** - 與備份組相關聯的備份原則或磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="dd24e-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="dd24e-118">**大小** - 備份組的實際大小。</span><span class="sxs-lookup"><span data-stu-id="dd24e-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="dd24e-119">**建立日期** - 建立備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="dd24e-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="dd24e-120">**類型** - 備份組可以是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="dd24e-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="dd24e-121">本機快照是本機儲存於裝置上的所有磁碟區資料備份，而雲端快照是指位於雲端的磁碟區資料備份。</span><span class="sxs-lookup"><span data-stu-id="dd24e-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="dd24e-122">本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="dd24e-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="dd24e-123">**啟動者** – 備份可由排程自動啟動，或由使用者手動啟動。</span><span class="sxs-lookup"><span data-stu-id="dd24e-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="dd24e-124">您可以使用備份原則排程備份。</span><span class="sxs-lookup"><span data-stu-id="dd24e-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="dd24e-125">或者，可以使用 [進行備份]  選項來進行手動備份。</span><span class="sxs-lookup"><span data-stu-id="dd24e-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="dd24e-126">列出磁碟區的備份組</span><span class="sxs-lookup"><span data-stu-id="dd24e-126">List backup sets for a volume</span></span>
<span data-ttu-id="dd24e-127">完成下列步驟，以列出磁碟區的所有備份。</span><span class="sxs-lookup"><span data-stu-id="dd24e-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="dd24e-128">若要列出備份組</span><span class="sxs-lookup"><span data-stu-id="dd24e-128">To list backup sets</span></span>
1. <span data-ttu-id="dd24e-129">在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dd24e-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="dd24e-130">如下方所示，篩選選取項目：</span><span class="sxs-lookup"><span data-stu-id="dd24e-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="dd24e-131">選取適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="dd24e-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="dd24e-132">在下拉式清單中，選擇要檢視對應備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="dd24e-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="dd24e-133">指定時間範圍。</span><span class="sxs-lookup"><span data-stu-id="dd24e-133">Specify the time range.</span></span>
   4. <span data-ttu-id="dd24e-134">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="dd24e-134">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="dd24e-136">以執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="dd24e-136">to execute this query.</span></span>
      
      <span data-ttu-id="dd24e-137">與選取的磁碟區相關的備份應會顯示在備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="dd24e-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="dd24e-138">選取備份組</span><span class="sxs-lookup"><span data-stu-id="dd24e-138">Select a backup set</span></span>
<span data-ttu-id="dd24e-139">完成下列步驟，選取磁碟區的備份組或備份原則。</span><span class="sxs-lookup"><span data-stu-id="dd24e-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="dd24e-140">若要選取備份組</span><span class="sxs-lookup"><span data-stu-id="dd24e-140">To select a backup set</span></span>
1. <span data-ttu-id="dd24e-141">在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dd24e-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="dd24e-142">如下方所示，篩選選取項目：</span><span class="sxs-lookup"><span data-stu-id="dd24e-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="dd24e-143">選取適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="dd24e-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="dd24e-144">在下拉式清單中，針對要選取的備份選擇磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="dd24e-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="dd24e-145">指定時間範圍。</span><span class="sxs-lookup"><span data-stu-id="dd24e-145">Specify the time range.</span></span>
   4. <span data-ttu-id="dd24e-146">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="dd24e-146">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="dd24e-148">以執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="dd24e-148">to execute this query.</span></span>
      
      <span data-ttu-id="dd24e-149">與選取的磁碟區或備份原則相關聯的備份應該會出現在備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="dd24e-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="dd24e-150">選取並展開備份組。</span><span class="sxs-lookup"><span data-stu-id="dd24e-150">Select and expand a backup set.</span></span> <span data-ttu-id="dd24e-151">[還原] 與 [刪除] 選項會顯示在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="dd24e-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="dd24e-152">您可以在選取的備份組上執行以上任一動作。</span><span class="sxs-lookup"><span data-stu-id="dd24e-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="dd24e-153">刪除備份組</span><span class="sxs-lookup"><span data-stu-id="dd24e-153">Delete a backup set</span></span>
<span data-ttu-id="dd24e-154">不再需要保留與備份相關的資料時，請將備份刪除。</span><span class="sxs-lookup"><span data-stu-id="dd24e-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="dd24e-155">執行下列步驟以刪除備份組。</span><span class="sxs-lookup"><span data-stu-id="dd24e-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="dd24e-156">若要刪除備份組</span><span class="sxs-lookup"><span data-stu-id="dd24e-156">To delete a backup set</span></span>
1. <span data-ttu-id="dd24e-157">請在 StorSimple Manager 服務頁面上，按一下 [備份類別目錄] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="dd24e-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="dd24e-158">如下方所示，篩選選取項目：</span><span class="sxs-lookup"><span data-stu-id="dd24e-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="dd24e-159">選取適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="dd24e-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="dd24e-160">在下拉式清單中，針對要選取的備份選擇磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="dd24e-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="dd24e-161">指定時間範圍。</span><span class="sxs-lookup"><span data-stu-id="dd24e-161">Specify the time range.</span></span>
   4. <span data-ttu-id="dd24e-162">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="dd24e-162">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="dd24e-164">以執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="dd24e-164">to execute this query.</span></span>
      
      <span data-ttu-id="dd24e-165">與選取的磁碟區或備份原則相關聯的備份應該會出現在備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="dd24e-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="dd24e-166">選取並展開備份組。</span><span class="sxs-lookup"><span data-stu-id="dd24e-166">Select and expand a backup set.</span></span> <span data-ttu-id="dd24e-167">[還原] 與 [刪除] 選項會顯示在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="dd24e-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="dd24e-168">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="dd24e-168">Click **Delete**.</span></span>
4. <span data-ttu-id="dd24e-169">刪除進行中和順利完成時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="dd24e-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="dd24e-170">刪除完成之後，重新整理此頁面上的查詢。</span><span class="sxs-lookup"><span data-stu-id="dd24e-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="dd24e-171">已刪除的備份組將不會再顯示於備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="dd24e-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd24e-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd24e-172">Next steps</span></span>
* <span data-ttu-id="dd24e-173">了解如何使用備份類別目錄以 [從備份組還原裝置](storsimple-restore-from-backup-set.md)。</span><span class="sxs-lookup"><span data-stu-id="dd24e-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="dd24e-174">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="dd24e-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

