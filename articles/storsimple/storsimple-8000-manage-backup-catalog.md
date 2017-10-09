---
title: "aaaManage 您 StorSimple 備份目錄 |Microsoft 文件"
description: "說明如何 toouse hello StorSimple 裝置管理員服務備份類別目錄 頁面 toolist 選取，並刪除備份組。"
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
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="b8057-103">使用 hello StorSimple 裝置管理員服務 toomanage 備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="b8057-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="b8057-104">概觀</span><span class="sxs-lookup"><span data-stu-id="b8057-104">Overview</span></span>
<span data-ttu-id="b8057-105">hello StorSimple 裝置管理員服務**備份類別目錄**刀鋒視窗會顯示所有手動或排程備份時，會建立 hello 備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="b8057-106">您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b8057-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="b8057-107">本教學課程說明如何 toolist、 select 和刪除的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="b8057-108">toolearn 如何 toorestore 從備份裝置跳過[從備份集還原您的裝置](storsimple-8000-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b8057-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="b8057-109">如何 tooclone 磁碟區，跳過 toolearn[複製 StorSimple 磁碟區](storsimple-8000-clone-volume-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b8057-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![備份類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="b8057-111">hello**備份類別目錄**刀鋒視窗中提供的查詢 toonarrow 備份組的選取項目。</span><span class="sxs-lookup"><span data-stu-id="b8057-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="b8057-112">您可以篩選 hello 備份組所擷取，根據下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8057-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="b8057-113">**裝置**– hello 裝置的 hello 當初建立備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="b8057-114">**備份原則或磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b8057-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="b8057-115">**From 和 To** – hello hello 備份集建立時的日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b8057-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="b8057-116">hello 篩選的備份組會再製成資料表根據 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b8057-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="b8057-117">**名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="b8057-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="b8057-118">**大小**– hello hello 備份組的實際大小。</span><span class="sxs-lookup"><span data-stu-id="b8057-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="b8057-119">**建立日期**– hello 日期和建立 hello 備份時的時間。</span><span class="sxs-lookup"><span data-stu-id="b8057-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="b8057-120">**類型** - 備份組可以是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="b8057-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="b8057-121">本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="b8057-122">本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="b8057-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="b8057-123">**起始者**– 由排程或手動使用者 hello 備份也可以自動初始化。</span><span class="sxs-lookup"><span data-stu-id="b8057-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="b8057-124">您可以使用備份原則 tooschedule 備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="b8057-125">或者，您可以使用 hello**取得備份**選項 tootake 手動備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="b8057-126">列出備份原則的備份組</span><span class="sxs-lookup"><span data-stu-id="b8057-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="b8057-127">完成下列步驟 toolist hello 所有 hello 備份的備份原則。</span><span class="sxs-lookup"><span data-stu-id="b8057-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="b8057-128">toolist 備份組</span><span class="sxs-lookup"><span data-stu-id="b8057-128">toolist backup sets</span></span>
1. <span data-ttu-id="b8057-129">移 tooyour StorSimple 裝置管理員服務，然後按一下**備份類別目錄**。</span><span class="sxs-lookup"><span data-stu-id="b8057-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="b8057-130">篩選 hello 選取項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8057-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="b8057-131">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b8057-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="b8057-132">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="b8057-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="b8057-133">依篩選**備份原則**tooview hello 對應 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="b8057-134">從 hello 備份原則下拉式清單中，選擇 **所有**tooview 所有 hello 上 hello 選取備份裝置。</span><span class="sxs-lookup"><span data-stu-id="b8057-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="b8057-135">按一下**套用**tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="b8057-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="b8057-136">備份組的 hello 清單應會顯示 hello 與 hello 選取備份原則相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="b8057-138">選取備份組</span><span class="sxs-lookup"><span data-stu-id="b8057-138">Select a backup set</span></span>
<span data-ttu-id="b8057-139">完成下列步驟 tooselect 的備份組的磁碟區或備份原則的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8057-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="b8057-140">tooselect 備份組</span><span class="sxs-lookup"><span data-stu-id="b8057-140">tooselect a backup set</span></span>
1. <span data-ttu-id="b8057-141">移 tooyour StorSimple 裝置管理員服務，然後按一下**備份類別目錄**。</span><span class="sxs-lookup"><span data-stu-id="b8057-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="b8057-142">篩選 hello 選取項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8057-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="b8057-143">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b8057-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="b8057-144">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="b8057-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="b8057-145">篩選您想 tooselect hello 備份的磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="b8057-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="b8057-146">按一下**套用**tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="b8057-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="b8057-147">hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="b8057-149">選取並展開備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-149">Select and expand a backup set.</span></span> <span data-ttu-id="b8057-150">您現在可以看到 hello 切分 hello 它所包含的磁碟區的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="b8057-151">hello**還原**和**刪除**選項都是透過 hello 備份組的 hello 操作功能表 （按一下滑鼠右鍵）。</span><span class="sxs-lookup"><span data-stu-id="b8057-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="b8057-152">您可以執行這些動作 hello 您選取的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="b8057-154">刪除備份組</span><span class="sxs-lookup"><span data-stu-id="b8057-154">Delete a backup set</span></span>
<span data-ttu-id="b8057-155">當您不再想與它相關聯的 tooretain hello 資料刪除的備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="b8057-156">執行下列步驟 toodelete 備份組的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8057-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="b8057-157">toodelete 備份組</span><span class="sxs-lookup"><span data-stu-id="b8057-157">toodelete a backup set</span></span>
 <span data-ttu-id="b8057-158">移 tooyour StorSimple 裝置管理員服務，然後按一下**備份類別目錄**。</span><span class="sxs-lookup"><span data-stu-id="b8057-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="b8057-159">篩選 hello 選取項目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8057-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="b8057-160">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="b8057-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="b8057-161">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="b8057-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="b8057-162">篩選您想 tooselect hello 備份的磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="b8057-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="b8057-163">按一下**套用**tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="b8057-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="b8057-164">hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="b8057-166">選取並展開備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-166">Select and expand a backup set.</span></span> <span data-ttu-id="b8057-167">您現在可以看到 hello 切分 hello 它所包含的磁碟區的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="b8057-168">hello**還原**和**刪除**選項都是透過 hello 備份組的 hello 操作功能表 （按一下滑鼠右鍵）。</span><span class="sxs-lookup"><span data-stu-id="b8057-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="b8057-169">以滑鼠右鍵按一下選取的 hello 備份組，然後從 hello 內容功能表中，選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8057-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="b8057-171">當提示確認，請檢閱 hello 顯示資訊，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8057-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="b8057-172">會永久刪除 hello 所選的備份。</span><span class="sxs-lookup"><span data-stu-id="b8057-172">hello selected backup is deleted permanently.</span></span>

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="b8057-174">當 hello 刪除正在進行時和順利完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="b8057-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="b8057-175">Hello 刪除完成之後，重新整理此頁面上的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="b8057-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="b8057-176">hello 刪除備份組不會再出現在 hello 清單中的備份組。</span><span class="sxs-lookup"><span data-stu-id="b8057-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="b8057-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8057-178">Next steps</span></span>
* <span data-ttu-id="b8057-179">了解如何太[使用 hello 備份類別目錄 toorestore 您的裝置，從備份集](storsimple-8000-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b8057-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="b8057-180">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="b8057-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

