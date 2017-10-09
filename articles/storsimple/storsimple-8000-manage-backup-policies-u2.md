---
title: "aaaManage StorSimple 8000 系列的備份原則 |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員服務 toocreate，及管理手動備份、 備份排程，以及備份保留在 StorSimple 8000 系列裝置上。"
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
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="acc85-103">在 Azure 入口網站 toomanage 備份原則中使用 hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="acc85-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="acc85-104">概觀</span><span class="sxs-lookup"><span data-stu-id="acc85-104">Overview</span></span>

<span data-ttu-id="acc85-105">本教學課程說明如何 toouse hello StorSimple 裝置管理員服務**備份原則**刀鋒視窗 toocontrol 備份程序和備份保留您的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="acc85-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="acc85-106">它也會說明如何 toocomplete 手動備份。</span><span class="sxs-lookup"><span data-stu-id="acc85-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="acc85-107">當您將備份磁碟區時，您可以選擇 toocreate 本機快照或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="acc85-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="acc85-108">如果您正在備份固定在本機的磁碟區，我們建議您指定雲端快照。</span><span class="sxs-lookup"><span data-stu-id="acc85-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="acc85-109">拍下大量的固定在本機的磁碟區的本機快照，再加上具大量變換的資料集，將會導致本機空間很快就不足的情況。</span><span class="sxs-lookup"><span data-stu-id="acc85-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="acc85-110">如果您選擇 tootake 本機快照集時，我們建議您 hello 最新狀態會佔用較少的每日快照集 tooback，它們保留每日，然後再刪除它們。</span><span class="sxs-lookup"><span data-stu-id="acc85-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="acc85-111">當本機固定磁碟區的雲端快照，您可以複製只有變更的 hello 資料 toohello 雲端，它是重複資料刪除和壓縮。</span><span class="sxs-lookup"><span data-stu-id="acc85-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="acc85-112">hello 備份原則 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="acc85-112">hello Backup policy blade</span></span>

<span data-ttu-id="acc85-113">hello**備份原則**StorSimple 裝置的刀鋒視窗可讓您 toomanage 備份原則排程本機和雲端快照。</span><span class="sxs-lookup"><span data-stu-id="acc85-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="acc85-114">備份原則不使用的 tooconfigure 備份排程和備份保留的磁碟區集合。</span><span class="sxs-lookup"><span data-stu-id="acc85-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="acc85-115">備份原則可讓您的多個磁碟區快照集 tootake 同時。</span><span class="sxs-lookup"><span data-stu-id="acc85-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="acc85-116">這表示建立的備份原則的 hello 備份將會損毀一致的複本。</span><span class="sxs-lookup"><span data-stu-id="acc85-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="acc85-117">hello 備份原則的表格式清單也可讓您 toofilter hello 現有的備份原則由一或多個 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="acc85-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="acc85-118">**原則名稱**– hello 與 hello 原則相關聯的名稱。</span><span class="sxs-lookup"><span data-stu-id="acc85-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="acc85-119">hello 不同類型的原則包括：</span><span class="sxs-lookup"><span data-stu-id="acc85-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="acc85-120">排程的原則，由 hello 使用者明確建立。</span><span class="sxs-lookup"><span data-stu-id="acc85-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="acc85-121">匯入原則，最初建立於 hello StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="acc85-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="acc85-122">這些具有描述 hello 原則匯入從 hello StorSimple Snapshot Manager 主控件的標記。</span><span class="sxs-lookup"><span data-stu-id="acc85-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="acc85-123">在建立磁碟區的 hello 階段不再啟用自動] 或 [預設的備份原則。</span><span class="sxs-lookup"><span data-stu-id="acc85-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="acc85-124">**上次成功備份**– hello 的日期和時間 hello 最後一個成功備份與此原則。</span><span class="sxs-lookup"><span data-stu-id="acc85-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="acc85-125">**下一次備份**– hello 的日期和時間 hello 下一個排定的備份將會起始此原則。</span><span class="sxs-lookup"><span data-stu-id="acc85-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="acc85-126">**磁碟區**– hello 與 hello 原則相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="acc85-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="acc85-127">建立備份時，會一起分組與備份原則相關聯的所有 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="acc85-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="acc85-128">**排程**– hello 的 hello 備份原則相關聯的排程數目。</span><span class="sxs-lookup"><span data-stu-id="acc85-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="acc85-129">您可以執行的備份原則的 hello 常用作業為：</span><span class="sxs-lookup"><span data-stu-id="acc85-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="acc85-130">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="acc85-130">Add a backup policy</span></span>
* <span data-ttu-id="acc85-131">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="acc85-131">Add or modify a schedule</span></span>
* <span data-ttu-id="acc85-132">新增或移除磁碟區</span><span class="sxs-lookup"><span data-stu-id="acc85-132">Add or remove a volume</span></span>
* <span data-ttu-id="acc85-133">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="acc85-133">Delete a backup policy</span></span>
* <span data-ttu-id="acc85-134">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="acc85-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="acc85-135">新增備份原則</span><span class="sxs-lookup"><span data-stu-id="acc85-135">Add a backup policy</span></span>

<span data-ttu-id="acc85-136">加入備份原則 tooautomatically 排程備份。</span><span class="sxs-lookup"><span data-stu-id="acc85-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="acc85-137">當您第一次建立磁碟區時，沒有與您的磁碟區相關聯的預設備份原則。</span><span class="sxs-lookup"><span data-stu-id="acc85-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="acc85-138">您需要 tooadd，並指定備份原則 tooprotect 磁碟區資料。</span><span class="sxs-lookup"><span data-stu-id="acc85-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="acc85-139">執行下列步驟在 hello Azure 入口網站 tooadd StorSimple 裝置的備份原則中的 hello。</span><span class="sxs-lookup"><span data-stu-id="acc85-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="acc85-140">您將加入 hello 原則之後，您可以定義排程 (請參閱[新增或修改排程](#add-or-modify-a-schedule))。</span><span class="sxs-lookup"><span data-stu-id="acc85-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="acc85-141">新增或修改排程</span><span class="sxs-lookup"><span data-stu-id="acc85-141">Add or modify a schedule</span></span>

<span data-ttu-id="acc85-142">您可以新增或修改附加的 tooan 備份原則存在您的 StorSimple 裝置上的排程。</span><span class="sxs-lookup"><span data-stu-id="acc85-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="acc85-143">執行下列步驟，在 Azure 入口網站 tooadd hello hello 或修改排程。</span><span class="sxs-lookup"><span data-stu-id="acc85-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="acc85-144">新增或移除磁碟區</span><span class="sxs-lookup"><span data-stu-id="acc85-144">Add or remove a volume</span></span>

<span data-ttu-id="acc85-145">您可以新增或移除磁碟區指派 tooa StorSimple 裝置上的備份原則。</span><span class="sxs-lookup"><span data-stu-id="acc85-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="acc85-146">執行下列步驟，在 Azure 入口網站 tooadd hello hello 或移除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="acc85-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="acc85-147">刪除備份原則</span><span class="sxs-lookup"><span data-stu-id="acc85-147">Delete a backup policy</span></span>

<span data-ttu-id="acc85-148">執行 hello 遵循您的 StorSimple 裝置上 hello Azure 入口網站 toodelete 備份原則中的步驟。</span><span class="sxs-lookup"><span data-stu-id="acc85-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="acc85-149">進行手動備份</span><span class="sxs-lookup"><span data-stu-id="acc85-149">Take a manual backup</span></span>

<span data-ttu-id="acc85-150">執行下列步驟，在單一磁碟區的 hello Azure 入口網站 toocreate 隨 （手動） 備份中的 hello。</span><span class="sxs-lookup"><span data-stu-id="acc85-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="acc85-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acc85-151">Next steps</span></span>

<span data-ttu-id="acc85-152">深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="acc85-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

