---
title: "管理 StorSimple 8000 系列備份原則 | Microsoft Docs"
description: "說明如何使用 StorSimple 裝置管理員服務在 StorSimple 8000 裝置上建立並管理手動備份、備份排程與備份保留。"
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 569dbfdeb7dcd526cb5a54b487ea1bfb59b13cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-manage-backup-policies"></a><span data-ttu-id="aa26e-103">在 Azure 入口網站中，使用 StorSimple 裝置管理員服務來管理備份原則</span><span class="sxs-lookup"><span data-stu-id="aa26e-103">Use the StorSimple Device Manager service in Azure portal to manage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="aa26e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="aa26e-104">Overview</span></span>

<span data-ttu-id="aa26e-105">本教學課程說明如何使用 StorSimple 裝置管理員服務的 [備份原則] 刀鋒視窗來控制 StorSimple 磁碟區的備份程序和備份保留。</span><span class="sxs-lookup"><span data-stu-id="aa26e-105">This tutorial explains how to use the StorSimple Device Manager service **Backup policy** blade to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="aa26e-106">它也會說明如何完成手動備份。</span><span class="sxs-lookup"><span data-stu-id="aa26e-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="aa26e-107">在您備份磁碟區時，您可以選擇建立本機快照或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="aa26e-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="aa26e-108">如果您正在備份固定在本機的磁碟區，我們建議您指定雲端快照。</span><span class="sxs-lookup"><span data-stu-id="aa26e-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="aa26e-109">拍下大量的固定在本機的磁碟區的本機快照，再加上具大量變換的資料集，將會導致本機空間很快就不足的情況。</span><span class="sxs-lookup"><span data-stu-id="aa26e-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="aa26e-110">如果您選擇建立本機快照，我們建議您拍下較少量的每日快照來備份最新的狀態，加以保留一天後再予以刪除。</span><span class="sxs-lookup"><span data-stu-id="aa26e-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="aa26e-111">針對固定在本機的磁碟區，在拍下雲端快照時，您僅會將變更的資料複製到雲端，並在其中將重複項目刪除及壓縮快照。</span><span class="sxs-lookup"><span data-stu-id="aa26e-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span>

## <a name="the-backup-policy-blade"></a><span data-ttu-id="aa26e-112">[備份原則] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="aa26e-112">The Backup policy blade</span></span>

<span data-ttu-id="aa26e-113">您的 StorSimple 裝置的 [備份原則] 刀鋒視窗可讓您管理備份原則並排程本機和雲端快照。</span><span class="sxs-lookup"><span data-stu-id="aa26e-113">The **Backup policy** blade for your StorSimple device allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="aa26e-114">備份原則用來設定磁碟區集合的備份排程和備份保留。</span><span class="sxs-lookup"><span data-stu-id="aa26e-114">Backup policies are used to configure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="aa26e-115">備份原則可讓您同時建立多個磁碟區的快照。</span><span class="sxs-lookup"><span data-stu-id="aa26e-115">Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="aa26e-116">這表示備份原則所建立的備份將會是與當機時一致的複本。</span><span class="sxs-lookup"><span data-stu-id="aa26e-116">This means that the backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="aa26e-117">備份原則表格式清單也可讓您依下列一個或多個欄位，篩選現有的備份原則：</span><span class="sxs-lookup"><span data-stu-id="aa26e-117">The backup policies tabular listing also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="aa26e-118">**原則名稱** – 與原則相關聯的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa26e-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="aa26e-119">不同類型的原則包括：</span><span class="sxs-lookup"><span data-stu-id="aa26e-119">The different types of policies include:</span></span>

  * <span data-ttu-id="aa26e-120">已排程的原則 (由使用者明確建立)。</span><span class="sxs-lookup"><span data-stu-id="aa26e-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="aa26e-121">匯入的原則 (原先是在 StorSimple Snapshot Manager 中所建立)。</span><span class="sxs-lookup"><span data-stu-id="aa26e-121">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="aa26e-122">這些包含說明從中匯入原則之 StorSimple Snapshot Manager 主機的標記。</span><span class="sxs-lookup"><span data-stu-id="aa26e-122">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aa26e-123">建立磁碟區時，不會再啟用自動或預設備份原則。</span><span class="sxs-lookup"><span data-stu-id="aa26e-123">Automatic or default backup policies are no longer enabled at the time of volume creation.</span></span>

* <span data-ttu-id="aa26e-124">**上一次成功的備份** – 使用此原則所進行的上一次成功備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="aa26e-124">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="aa26e-125">**下一次備份** – 此原則將起始的下一次排定的備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="aa26e-125">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="aa26e-126">**磁碟區** – 與原則相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="aa26e-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="aa26e-127">建立備份時，會將與備份原則相關聯的所有磁碟區群組在一起。</span><span class="sxs-lookup"><span data-stu-id="aa26e-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="aa26e-128">**排程** – 與備份原則相關聯的排程數目。</span><span class="sxs-lookup"><span data-stu-id="aa26e-128">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="aa26e-129">您可以執行的備份原則常用作業包括：</span><span class="sxs-lookup"><span data-stu-id="aa26e-129">The frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="aa26e-130">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="aa26e-130">Add a backup policy</span></span>
* <span data-ttu-id="aa26e-131">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="aa26e-131">Add or modify a schedule</span></span>
* <span data-ttu-id="aa26e-132">新增或移除磁碟區</span><span class="sxs-lookup"><span data-stu-id="aa26e-132">Add or remove a volume</span></span>
* <span data-ttu-id="aa26e-133">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="aa26e-133">Delete a backup policy</span></span>
* <span data-ttu-id="aa26e-134">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="aa26e-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="aa26e-135">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="aa26e-135">Add a backup policy</span></span>

<span data-ttu-id="aa26e-136">新增備份原則，以自動排程備份。</span><span class="sxs-lookup"><span data-stu-id="aa26e-136">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="aa26e-137">當您第一次建立磁碟區時，沒有與您的磁碟區相關聯的預設備份原則。</span><span class="sxs-lookup"><span data-stu-id="aa26e-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="aa26e-138">您必須新增並指派備份原則以保護磁碟區資料。</span><span class="sxs-lookup"><span data-stu-id="aa26e-138">You need to add and assign a backup policy to protect volume data.</span></span>

<span data-ttu-id="aa26e-139">在 Azure 入口網站中執行下列步驟，以便為 StorSimple 裝置新增備份原則。</span><span class="sxs-lookup"><span data-stu-id="aa26e-139">Perform the following steps in the Azure portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="aa26e-140">新增原則之後，您可以定義排程 (請參閱 [新增或修改排程](#add-or-modify-a-schedule))。</span><span class="sxs-lookup"><span data-stu-id="aa26e-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="aa26e-141">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="aa26e-141">Add or modify a schedule</span></span>

<span data-ttu-id="aa26e-142">您可以在 StorSimple 裝置上新增或修改附加到現有備份原則的排程。</span><span class="sxs-lookup"><span data-stu-id="aa26e-142">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="aa26e-143">在 Azure 入口網站中執行下列步驟，以新增或修改排程。</span><span class="sxs-lookup"><span data-stu-id="aa26e-143">Perform the following steps in the Azure portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="aa26e-144">新增或移除磁碟區</span><span class="sxs-lookup"><span data-stu-id="aa26e-144">Add or remove a volume</span></span>

<span data-ttu-id="aa26e-145">您可以在 StorSimple 裝置上新增或移除指派至備份原則的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="aa26e-145">You can add or remove a volume assigned to a backup policy on your StorSimple device.</span></span> <span data-ttu-id="aa26e-146">在 Azure 入口網站中執行下列步驟，以新增或移除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="aa26e-146">Perform the following steps in the Azure portal to add or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="aa26e-147">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="aa26e-147">Delete a backup policy</span></span>

<span data-ttu-id="aa26e-148">在 Azure 入口網站中執行下列步驟，以便刪除 StorSimple 裝置上的備份原則。</span><span class="sxs-lookup"><span data-stu-id="aa26e-148">Perform the following steps in the Azure portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="aa26e-149">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="aa26e-149">Take a manual backup</span></span>

<span data-ttu-id="aa26e-150">在 Azure 入口網站中執行下列步驟，以針對單一磁碟區建立隨選 (手動) 備份。</span><span class="sxs-lookup"><span data-stu-id="aa26e-150">Perform the following steps in the Azure portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="aa26e-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa26e-151">Next steps</span></span>

<span data-ttu-id="aa26e-152">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="aa26e-152">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

