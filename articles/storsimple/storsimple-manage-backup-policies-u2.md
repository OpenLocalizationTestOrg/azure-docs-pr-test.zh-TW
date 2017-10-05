---
title: "管理您的 StorSimple 備份原則 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 服務建立並管理手動備份、備份排程與備份保留。"
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
ms.openlocfilehash: 5448247428ab96887470c6b53f7a9b3dcd9238f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies-update-2"></a><span data-ttu-id="8866f-103">使用 StorSimple Manager 服務管理備份原則 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="8866f-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="8866f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8866f-104">Overview</span></span>
<span data-ttu-id="8866f-105">本教學課程說明如何使用 StorSimple Manager 服務的 [備份原則]  頁面控制 StorSimple 磁碟區的備份程序和備份保留。</span><span class="sxs-lookup"><span data-stu-id="8866f-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="8866f-106">它也會說明如何完成手動備份。</span><span class="sxs-lookup"><span data-stu-id="8866f-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="8866f-107">在您備份磁碟區時，您可以選擇建立本機快照或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="8866f-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="8866f-108">如果您正在備份固定在本機的磁碟區，我們建議您指定雲端快照。</span><span class="sxs-lookup"><span data-stu-id="8866f-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="8866f-109">拍下大量的固定在本機的磁碟區的本機快照，再加上具大量變換的資料集，將會導致本機空間很快就不足的情況。</span><span class="sxs-lookup"><span data-stu-id="8866f-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="8866f-110">如果您選擇建立本機快照，我們建議您拍下較少量的每日快照來備份最新的狀態，加以保留一天後再予以刪除。</span><span class="sxs-lookup"><span data-stu-id="8866f-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="8866f-111">針對固定在本機的磁碟區，在拍下雲端快照時，您僅會將變更的資料複製到雲端，並在其中將重複項目刪除及壓縮快照。</span><span class="sxs-lookup"><span data-stu-id="8866f-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span> 

## <a name="the-backup-policies-page"></a><span data-ttu-id="8866f-112">備份原則頁面</span><span class="sxs-lookup"><span data-stu-id="8866f-112">The Backup Policies page</span></span>
<span data-ttu-id="8866f-113">[備份原則] 頁面可讓您管理備份原則並排程本機和雲端快照 </span><span class="sxs-lookup"><span data-stu-id="8866f-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="8866f-114">(備份原則用來設定磁碟區集合的備份排程和備份保留)。備份原則可讓您同時建立多個磁碟區的快照。</span><span class="sxs-lookup"><span data-stu-id="8866f-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="8866f-115">這表示備份原則所建立的備份將會是與當機時一致的複本。</span><span class="sxs-lookup"><span data-stu-id="8866f-115">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="8866f-116">**備份原則頁面**會列出備份原則、其類型、相關聯的磁碟區、保留的備份數目，以及啟用這些原則的選項。</span><span class="sxs-lookup"><span data-stu-id="8866f-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="8866f-117">[備份原則]  頁面也可讓您依下列一個或多個欄位，篩選現有的備份原則：</span><span class="sxs-lookup"><span data-stu-id="8866f-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="8866f-118">**原則名稱** – 與原則相關聯的名稱。</span><span class="sxs-lookup"><span data-stu-id="8866f-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="8866f-119">不同類型的原則包括：</span><span class="sxs-lookup"><span data-stu-id="8866f-119">The different types of policies include:</span></span>
  
  * <span data-ttu-id="8866f-120">已排程的原則 (由使用者明確建立)。</span><span class="sxs-lookup"><span data-stu-id="8866f-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="8866f-121">自動原則 (建立磁碟區時啟用此磁碟區選項的預設備份時所建立)。</span><span class="sxs-lookup"><span data-stu-id="8866f-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="8866f-122">這些原則會被命名為 VolumeName_Default，其中 VolumeName 指的是 Azure 傳統入口網站中使用者所設定之 StorSimple 磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="8866f-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="8866f-123">自動原則會導致每日雲端快照於 22:30 裝置時間開始。</span><span class="sxs-lookup"><span data-stu-id="8866f-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="8866f-124">匯入的原則 (原先是在 StorSimple Snapshot Manager 中所建立)。</span><span class="sxs-lookup"><span data-stu-id="8866f-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="8866f-125">這些包含說明從中匯入原則之 StorSimple Snapshot Manager 主機的標記。</span><span class="sxs-lookup"><span data-stu-id="8866f-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="8866f-126">**磁碟區** – 與原則相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="8866f-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="8866f-127">建立備份時，會將與備份原則相關聯的所有磁碟區群組在一起。</span><span class="sxs-lookup"><span data-stu-id="8866f-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="8866f-128">**上一次成功的備份** – 使用此原則所進行的上一次成功備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="8866f-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="8866f-129">**下一次備份** – 此原則將起始的下一次排定的備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="8866f-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="8866f-130">**排程** – 與備份原則相關聯的排程數目。</span><span class="sxs-lookup"><span data-stu-id="8866f-130">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="8866f-131">您可以從這個頁面執行的常用作業包括：</span><span class="sxs-lookup"><span data-stu-id="8866f-131">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="8866f-132">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="8866f-132">Add a backup policy</span></span> 
* <span data-ttu-id="8866f-133">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="8866f-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="8866f-134">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="8866f-134">Delete a backup policy</span></span> 
* <span data-ttu-id="8866f-135">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="8866f-135">Take a manual backup</span></span> 
* <span data-ttu-id="8866f-136">建立具有多個磁碟區和排程的自訂備份原則</span><span class="sxs-lookup"><span data-stu-id="8866f-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="8866f-137">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="8866f-137">Add a backup policy</span></span>
<span data-ttu-id="8866f-138">新增備份原則，以自動排程備份。</span><span class="sxs-lookup"><span data-stu-id="8866f-138">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="8866f-139">在 Azure 傳統入口網站中執行下列步驟，以便為 StorSimple 裝置新增備份原則。</span><span class="sxs-lookup"><span data-stu-id="8866f-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="8866f-140">新增原則之後，您可以定義排程 (請參閱 [新增或修改排程](#add-or-modify-a-schedule))。</span><span class="sxs-lookup"><span data-stu-id="8866f-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="8866f-141">![提供的影片](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="8866f-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="8866f-142">若要觀看影片示範如何建立本機或雲端備份原則，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/)。</span><span class="sxs-lookup"><span data-stu-id="8866f-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="8866f-143">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="8866f-143">Add or modify a schedule</span></span>
<span data-ttu-id="8866f-144">您可以在 StorSimple 裝置上新增或修改附加到現有備份原則的排程。</span><span class="sxs-lookup"><span data-stu-id="8866f-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="8866f-145">在 Azure 傳統入口網站中執行下列步驟，以新增或修改排程。</span><span class="sxs-lookup"><span data-stu-id="8866f-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="8866f-146">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="8866f-146">Delete a backup policy</span></span>
<span data-ttu-id="8866f-147">在 Azure 傳統入口網站中執行下列步驟，以便刪除 StorSimple 裝置上的備份原則。</span><span class="sxs-lookup"><span data-stu-id="8866f-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="8866f-148">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="8866f-148">Take a manual backup</span></span>
<span data-ttu-id="8866f-149">在 Azure 傳統入口網站中執行下列步驟，以針對單一磁碟區建立隨選 (手動) 備份。</span><span class="sxs-lookup"><span data-stu-id="8866f-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="8866f-150">建立具有多個磁碟區和排程的自訂備份原則</span><span class="sxs-lookup"><span data-stu-id="8866f-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="8866f-151">在 Azure 傳統入口網站中執行下列步驟，以建立具有多個磁碟區和排程的自訂備份原則。</span><span class="sxs-lookup"><span data-stu-id="8866f-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="8866f-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8866f-152">Next steps</span></span>
<span data-ttu-id="8866f-153">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="8866f-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

