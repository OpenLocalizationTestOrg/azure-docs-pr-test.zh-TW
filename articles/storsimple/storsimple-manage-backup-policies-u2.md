---
title: "aaaManage 您 StorSimple 備份原則 |Microsoft 文件"
description: "說明如何使用 hello StorSimple Manager 服務 toocreate，及管理手動備份、 備份排程，以及備份保留。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="17c3c-103">使用 hello StorSimple Manager 服務 toomanage 備份原則 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="17c3c-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="17c3c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="17c3c-104">Overview</span></span>
<span data-ttu-id="17c3c-105">本教學課程說明如何 toouse hello StorSimple Manager 服務**備份原則**toocontrol 備份程序和為您的 StorSimple 磁碟區的備份保留頁面上。</span><span class="sxs-lookup"><span data-stu-id="17c3c-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="17c3c-106">它也會說明如何 toocomplete 手動備份。</span><span class="sxs-lookup"><span data-stu-id="17c3c-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="17c3c-107">當您將備份磁碟區時，您可以選擇 toocreate 本機快照或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="17c3c-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="17c3c-108">如果您正在備份固定在本機的磁碟區，我們建議您指定雲端快照。</span><span class="sxs-lookup"><span data-stu-id="17c3c-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="17c3c-109">拍下大量的固定在本機的磁碟區的本機快照，再加上具大量變換的資料集，將會導致本機空間很快就不足的情況。</span><span class="sxs-lookup"><span data-stu-id="17c3c-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="17c3c-110">如果您選擇 tootake 本機快照集時，我們建議您 hello 最新狀態會佔用較少的每日快照集 tooback，它們保留每日，然後再刪除它們。</span><span class="sxs-lookup"><span data-stu-id="17c3c-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="17c3c-111">當本機固定磁碟區的雲端快照，您可以複製只有變更的 hello 資料 toohello 雲端，它是重複資料刪除和壓縮。</span><span class="sxs-lookup"><span data-stu-id="17c3c-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="17c3c-112">hello 備份原則 頁面</span><span class="sxs-lookup"><span data-stu-id="17c3c-112">hello Backup Policies page</span></span>
<span data-ttu-id="17c3c-113">hello**備份原則**頁面可讓您 toomanage 備份原則排程本機和雲端快照。</span><span class="sxs-lookup"><span data-stu-id="17c3c-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="17c3c-114">（備份原則是使用的 tooconfigure 備份排程和備份保留磁碟區的集合）。備份原則可讓您的多個磁碟區快照集 tootake 同時。</span><span class="sxs-lookup"><span data-stu-id="17c3c-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="17c3c-115">這表示建立的備份原則的 hello 備份將會損毀一致的複本。</span><span class="sxs-lookup"><span data-stu-id="17c3c-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="17c3c-116">hello**備份原則**hello 備份原則、 其類型、 相關聯的 hello 磁碟區、 hello 數目的備份保留，頁面會列出與 hello 選項 tooenable 這些原則。</span><span class="sxs-lookup"><span data-stu-id="17c3c-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="17c3c-117">hello**備份原則**頁面也可讓您 toofilter hello 現有的備份原則的一或多個 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="17c3c-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="17c3c-118">**原則名稱**– hello 與 hello 原則相關聯的名稱。</span><span class="sxs-lookup"><span data-stu-id="17c3c-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="17c3c-119">hello 不同類型的原則包括：</span><span class="sxs-lookup"><span data-stu-id="17c3c-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="17c3c-120">排程的原則，由 hello 使用者明確建立。</span><span class="sxs-lookup"><span data-stu-id="17c3c-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="17c3c-121">自動原則，會建立 hello 這個磁碟區選項的預設備份的磁碟區建立 hello 次啟用時。</span><span class="sxs-lookup"><span data-stu-id="17c3c-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="17c3c-122">這些原則會命名為*VolumeName*_Default 其中*VolumeName*參考 toohello hello hello Azure 傳統入口網站中的 hello 使用者所設定的 StorSimple 磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="17c3c-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="17c3c-123">hello 自動原則會導致每日開始時間 22:30 裝置的雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="17c3c-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="17c3c-124">匯入原則，最初建立於 hello StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="17c3c-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="17c3c-125">這些具有描述 hello 原則匯入從 hello StorSimple Snapshot Manager 主控件的標記。</span><span class="sxs-lookup"><span data-stu-id="17c3c-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="17c3c-126">**磁碟區**– hello 與 hello 原則相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="17c3c-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="17c3c-127">建立備份時，會一起分組與備份原則相關聯的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="17c3c-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="17c3c-128">**上次成功備份**– hello 的日期和時間 hello 最後一個成功備份與此原則。</span><span class="sxs-lookup"><span data-stu-id="17c3c-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="17c3c-129">**下一次備份**– hello 的日期和時間 hello 下一個排定的備份將會起始此原則。</span><span class="sxs-lookup"><span data-stu-id="17c3c-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="17c3c-130">**排程**– hello 的 hello 備份原則相關聯的排程數目。</span><span class="sxs-lookup"><span data-stu-id="17c3c-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="17c3c-131">您可以從這個頁面上執行的常用的 hello 作業為：</span><span class="sxs-lookup"><span data-stu-id="17c3c-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="17c3c-132">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="17c3c-132">Add a backup policy</span></span> 
* <span data-ttu-id="17c3c-133">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="17c3c-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="17c3c-134">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="17c3c-134">Delete a backup policy</span></span> 
* <span data-ttu-id="17c3c-135">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="17c3c-135">Take a manual backup</span></span> 
* <span data-ttu-id="17c3c-136">建立具有多個磁碟區和排程的自訂備份原則</span><span class="sxs-lookup"><span data-stu-id="17c3c-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="17c3c-137">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="17c3c-137">Add a backup policy</span></span>
<span data-ttu-id="17c3c-138">加入備份原則 tooautomatically 排程備份。</span><span class="sxs-lookup"><span data-stu-id="17c3c-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="17c3c-139">執行下列步驟在 hello Azure 傳統入口網站 tooadd StorSimple 裝置的備份原則中的 hello。</span><span class="sxs-lookup"><span data-stu-id="17c3c-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="17c3c-140">您將加入 hello 原則之後，您可以定義排程 (請參閱[新增或修改排程](#add-or-modify-a-schedule))。</span><span class="sxs-lookup"><span data-stu-id="17c3c-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="17c3c-141">![提供的影片](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="17c3c-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="17c3c-142">toowatch 的視訊示範 toocreate 本機或雲端備份原則，按一下[這裡](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)。</span><span class="sxs-lookup"><span data-stu-id="17c3c-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="17c3c-143">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="17c3c-143">Add or modify a schedule</span></span>
<span data-ttu-id="17c3c-144">您可以新增或修改附加的 tooan 備份原則存在您的 StorSimple 裝置上的排程。</span><span class="sxs-lookup"><span data-stu-id="17c3c-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="17c3c-145">執行下列步驟在 hello Azure 傳統入口網站 tooadd hello 或修改排程。</span><span class="sxs-lookup"><span data-stu-id="17c3c-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="17c3c-146">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="17c3c-146">Delete a backup policy</span></span>
<span data-ttu-id="17c3c-147">執行 hello 遵循您的 StorSimple 裝置上 hello Azure 傳統入口網站 toodelete 備份原則中的步驟。</span><span class="sxs-lookup"><span data-stu-id="17c3c-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="17c3c-148">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="17c3c-148">Take a manual backup</span></span>
<span data-ttu-id="17c3c-149">執行下列步驟，在單一磁碟區的 hello Azure 傳統入口網站 toocreate 隨 （手動） 備份中的 hello。</span><span class="sxs-lookup"><span data-stu-id="17c3c-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="17c3c-150">建立具有多個磁碟區和排程的自訂備份原則</span><span class="sxs-lookup"><span data-stu-id="17c3c-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="17c3c-151">執行下列步驟在 hello Azure 傳統入口網站 toocreate 具有多個磁碟區和排程的自訂備份原則中的 hello。</span><span class="sxs-lookup"><span data-stu-id="17c3c-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="17c3c-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17c3c-152">Next steps</span></span>
<span data-ttu-id="17c3c-153">深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="17c3c-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

