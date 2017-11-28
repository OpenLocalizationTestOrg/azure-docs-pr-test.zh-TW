---
title: "aaaRestore StorSimple 磁碟區從備份 |Microsoft 文件"
description: "說明如何 toouse 會 hello StorSimple Manager 服務備份類別目錄 頁面 toorestore StorSimple 磁碟區從備份組。"
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
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="c0f44-103">從備份組還原 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="c0f44-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="c0f44-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c0f44-104">Overview</span></span>
<span data-ttu-id="c0f44-105">hello**備份類別目錄**頁面會顯示所有 hello 的備份組時手動或自動備份所建立的。</span><span class="sxs-lookup"><span data-stu-id="c0f44-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="c0f44-106">您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c0f44-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![備份類別目錄頁面](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="c0f44-108">本教學課程說明如何 toouse hello**備份類別目錄**頁面 toorestore 備份組中的裝置上的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c0f44-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="c0f44-109">如何 toouse hello 備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="c0f44-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="c0f44-110">hello**備份類別目錄**頁面會提供可協助您 toonarrow 查詢您的備份組選項。</span><span class="sxs-lookup"><span data-stu-id="c0f44-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="c0f44-111">您可以篩選 hello 的備份組會擷取根據 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="c0f44-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="c0f44-112">**裝置**– hello 裝置的 hello 當初建立備份組。</span><span class="sxs-lookup"><span data-stu-id="c0f44-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="c0f44-113">**備份原則**或**磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c0f44-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="c0f44-114">**從**和**至**– hello hello 備份集建立時的日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c0f44-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="c0f44-115">hello 篩選的備份組會再製成資料表根據 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c0f44-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="c0f44-116">**名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="c0f44-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="c0f44-117">**大小**– hello hello 備份組的實際大小。</span><span class="sxs-lookup"><span data-stu-id="c0f44-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="c0f44-118">**在建立**– hello 日期和建立 hello 備份時的時間。</span><span class="sxs-lookup"><span data-stu-id="c0f44-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="c0f44-119">**類型** - 備份組可以是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="c0f44-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="c0f44-120">本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。</span><span class="sxs-lookup"><span data-stu-id="c0f44-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="c0f44-121">本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="c0f44-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="c0f44-122">**由起始**– hello 備份可以自動根據 tooa 排程起始或由使用者手動。</span><span class="sxs-lookup"><span data-stu-id="c0f44-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="c0f44-123">（您可以使用備份原則 tooschedule 備份。</span><span class="sxs-lookup"><span data-stu-id="c0f44-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="c0f44-124">或者，您可以使用 hello**取得備份**選項 tootake 互動式備份。)</span><span class="sxs-lookup"><span data-stu-id="c0f44-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="c0f44-125">如何 toorestore 您的 StorSimple 磁碟區從備份</span><span class="sxs-lookup"><span data-stu-id="c0f44-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="c0f44-126">您可以使用 hello**備份類別目錄**頁面 toorestore 您的 StorSimple 磁碟區，從特定的備份。</span><span class="sxs-lookup"><span data-stu-id="c0f44-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="c0f44-127">從備份還原，將會取代 hello hello 備份中的現有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c0f44-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="c0f44-128">這也可能造成 hello hello 備份後寫入任何資料遺失。</span><span class="sxs-lookup"><span data-stu-id="c0f44-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="c0f44-129">初始化磁碟區上的還原之前，請確定 hello 磁碟區已離線。</span><span class="sxs-lookup"><span data-stu-id="c0f44-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="c0f44-130">您將需要 tootake hello 上的磁碟區離線 hello 主機第一次，然後 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="c0f44-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="c0f44-131">中的 hello 步驟[使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)。</span><span class="sxs-lookup"><span data-stu-id="c0f44-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="c0f44-132">執行下列步驟 toorestore 磁碟區從備份組的 hello。</span><span class="sxs-lookup"><span data-stu-id="c0f44-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="c0f44-133">從備份集 toorestore</span><span class="sxs-lookup"><span data-stu-id="c0f44-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="c0f44-134">在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c0f44-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![備份類別目錄](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="c0f44-136">選取備份組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0f44-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="c0f44-137">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="c0f44-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="c0f44-138">在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="c0f44-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="c0f44-139">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c0f44-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="c0f44-140">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="c0f44-140">Click hello check icon</span></span> ![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="c0f44-142">tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="c0f44-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="c0f44-143">hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。</span><span class="sxs-lookup"><span data-stu-id="c0f44-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="c0f44-144">展開 hello 備份組 tooview hello 相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c0f44-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="c0f44-145">這些磁碟區必須採取 hello 主機和裝置上離線再進行還原。</span><span class="sxs-lookup"><span data-stu-id="c0f44-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="c0f44-146">中的 hello 步驟[使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)。</span><span class="sxs-lookup"><span data-stu-id="c0f44-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c0f44-147">請確定您已經執行 hello 磁碟區離線 hello 主機上的第一次之後您才能 hello 裝置上的 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="c0f44-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="c0f44-148">如果您不會在 hello 主機上取得 hello 磁碟區離線，有可能導致 toodata 損毀。</span><span class="sxs-lookup"><span data-stu-id="c0f44-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="c0f44-149">選取備份組。</span><span class="sxs-lookup"><span data-stu-id="c0f44-149">Select a backup set.</span></span> <span data-ttu-id="c0f44-150">按一下**還原**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="c0f44-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="c0f44-151">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="c0f44-151">You will be prompted for confirmation.</span></span> 
   
    ![確認電子郵件](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="c0f44-153">檢閱 hello 還原資訊，然後按一下核取圖示，hello![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png)。</span><span class="sxs-lookup"><span data-stu-id="c0f44-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="c0f44-154">這會起始的還原作業，您可以藉由存取 hello 檢視**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="c0f44-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="c0f44-155">Hello 還原完成後，您可以確認您的磁碟區 hello 內容會取代從 hello 備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="c0f44-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="c0f44-156">![提供的影片](./media/storsimple-restore-from-backup-set/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="c0f44-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="c0f44-157">toowatch 的影片示範如何使用 hello 複製和還原功能在 StorSimple toorecover 刪除檔案中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="c0f44-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0f44-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0f44-158">Next steps</span></span>
* <span data-ttu-id="c0f44-159">了解如何太[管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="c0f44-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="c0f44-160">了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="c0f44-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

