---
title: "aaaManage 您 StorSimple 備份目錄 |Microsoft 文件"
description: "說明如何 toouse hello StorSimple Manager 服務備份類別目錄 頁面 toolist，選取，並刪除磁碟區的備份組。"
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
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="0056f-103">使用 hello StorSimple Manager 服務 toomanage 備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="0056f-103">Use hello StorSimple Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="0056f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0056f-104">Overview</span></span>
<span data-ttu-id="0056f-105">StorSimple Manager 服務的 hello**備份類別目錄**頁面會顯示所有手動或排程備份時，會建立 hello 備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="0056f-106">您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0056f-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="0056f-107">本教學課程說明如何 toolist、 select 和刪除的備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="0056f-108">toolearn 如何 toorestore 從備份裝置跳過[從備份集還原您的裝置](storsimple-restore-from-backup-set.md)。</span><span class="sxs-lookup"><span data-stu-id="0056f-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="0056f-109">如何 tooclone 磁碟區，跳過 toolearn[複製 StorSimple 磁碟區](storsimple-clone-volume.md)。</span><span class="sxs-lookup"><span data-stu-id="0056f-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![備份類別目錄](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="0056f-111">hello**備份類別目錄**頁面會提供查詢 toonarrow 備份組的選取項目。</span><span class="sxs-lookup"><span data-stu-id="0056f-111">hello **Backup Catalog** page provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="0056f-112">您可以篩選 hello 備份組所擷取，根據下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="0056f-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="0056f-113">**裝置**– hello 裝置的 hello 當初建立備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="0056f-114">**備份原則或磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0056f-114">**Backup Policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="0056f-115">**From 和 To** – hello hello 備份集建立時的日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="0056f-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="0056f-116">hello 篩選的備份組會再製成資料表根據 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0056f-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="0056f-117">**名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="0056f-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="0056f-118">**大小**– hello hello 備份組的實際大小。</span><span class="sxs-lookup"><span data-stu-id="0056f-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="0056f-119">**建立日期**– hello 日期和建立 hello 備份時的時間。</span><span class="sxs-lookup"><span data-stu-id="0056f-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="0056f-120">**類型** - 備份組可以是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="0056f-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="0056f-121">本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。</span><span class="sxs-lookup"><span data-stu-id="0056f-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="0056f-122">本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="0056f-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="0056f-123">**起始者**– 由排程或手動使用者 hello 備份也可以自動初始化。</span><span class="sxs-lookup"><span data-stu-id="0056f-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="0056f-124">您可以使用備份原則 tooschedule 備份。</span><span class="sxs-lookup"><span data-stu-id="0056f-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="0056f-125">或者，您可以使用 hello**取得備份**選項 tootake 手動備份。</span><span class="sxs-lookup"><span data-stu-id="0056f-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="0056f-126">列出磁碟區的備份組</span><span class="sxs-lookup"><span data-stu-id="0056f-126">List backup sets for a volume</span></span>
<span data-ttu-id="0056f-127">完成下列步驟 toolist hello 所有 hello 備份磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0056f-127">Complete hello following steps toolist all hello backups for a volume.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="0056f-128">toolist 備份組</span><span class="sxs-lookup"><span data-stu-id="0056f-128">toolist backup sets</span></span>
1. <span data-ttu-id="0056f-129">在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0056f-129">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="0056f-130">篩選 hello 選取項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0056f-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="0056f-131">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="0056f-131">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="0056f-132">在 [hello] 下拉式清單中，選擇磁碟區 tooview hello 對應 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="0056f-132">In hello drop-down list, choose a volume tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="0056f-133">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="0056f-133">Specify hello time range.</span></span>
   4. <span data-ttu-id="0056f-134">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="0056f-134">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="0056f-136">tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="0056f-136">tooexecute this query.</span></span>
      
      <span data-ttu-id="0056f-137">備份組的 hello 清單應會顯示 hello 與 hello 選取磁碟區相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="0056f-137">hello backups associated with hello selected volume should appear in hello list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="0056f-138">選取備份組</span><span class="sxs-lookup"><span data-stu-id="0056f-138">Select a backup set</span></span>
<span data-ttu-id="0056f-139">完成下列步驟 tooselect 的備份組的磁碟區或備份原則的 hello。</span><span class="sxs-lookup"><span data-stu-id="0056f-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="0056f-140">tooselect 備份組</span><span class="sxs-lookup"><span data-stu-id="0056f-140">tooselect a backup set</span></span>
1. <span data-ttu-id="0056f-141">在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0056f-141">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="0056f-142">篩選 hello 選取項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0056f-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="0056f-143">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="0056f-143">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="0056f-144">在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="0056f-144">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="0056f-145">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="0056f-145">Specify hello time range.</span></span>
   4. <span data-ttu-id="0056f-146">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="0056f-146">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="0056f-148">tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="0056f-148">tooexecute this query.</span></span>
      
      <span data-ttu-id="0056f-149">hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-149">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="0056f-150">選取並展開備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-150">Select and expand a backup set.</span></span> <span data-ttu-id="0056f-151">hello**還原**和**刪除**選項會顯示在 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="0056f-151">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="0056f-152">您可以執行這些動作 hello 您選取的備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-152">You can perform either of these actions on hello backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="0056f-153">刪除備份組</span><span class="sxs-lookup"><span data-stu-id="0056f-153">Delete a backup set</span></span>
<span data-ttu-id="0056f-154">當您不再想與它相關聯的 tooretain hello 資料刪除的備份。</span><span class="sxs-lookup"><span data-stu-id="0056f-154">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="0056f-155">執行下列步驟 toodelete 備份組的 hello。</span><span class="sxs-lookup"><span data-stu-id="0056f-155">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="0056f-156">toodelete 備份組</span><span class="sxs-lookup"><span data-stu-id="0056f-156">toodelete a backup set</span></span>
1. <span data-ttu-id="0056f-157">在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄] 索引標籤**。</span><span class="sxs-lookup"><span data-stu-id="0056f-157">On hello StorSimple Manager service page, click hello **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="0056f-158">篩選 hello 選取項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0056f-158">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="0056f-159">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="0056f-159">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="0056f-160">在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="0056f-160">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="0056f-161">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="0056f-161">Specify hello time range.</span></span>
   4. <span data-ttu-id="0056f-162">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="0056f-162">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="0056f-164">tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="0056f-164">tooexecute this query.</span></span>
      
      <span data-ttu-id="0056f-165">hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-165">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="0056f-166">選取並展開備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-166">Select and expand a backup set.</span></span> <span data-ttu-id="0056f-167">hello**還原**和**刪除**選項會顯示在 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="0056f-167">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="0056f-168">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="0056f-168">Click **Delete**.</span></span>
4. <span data-ttu-id="0056f-169">當 hello 刪除正在進行時和順利完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="0056f-169">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="0056f-170">Hello 刪除完成之後，重新整理此頁面上的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="0056f-170">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="0056f-171">hello 刪除備份組不會再出現在 hello 清單中的備份組。</span><span class="sxs-lookup"><span data-stu-id="0056f-171">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0056f-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0056f-172">Next steps</span></span>
* <span data-ttu-id="0056f-173">了解如何太[使用 hello 備份類別目錄 toorestore 您的裝置，從備份集](storsimple-restore-from-backup-set.md)。</span><span class="sxs-lookup"><span data-stu-id="0056f-173">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="0056f-174">了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="0056f-174">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

