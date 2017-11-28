---
title: "在 StorSimple 8000 系列上從備份還原磁碟區 | Microsoft Docs"
description: "說明如何使用 StorSimple 裝置管理員服務的 [備份類別目錄]，從備份組還原 StorSimple 磁碟區。"
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: aff0710ead4f76bb80c38e2d88fe9cd3ce6a7b48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="fc390-103">從備份組還原 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="fc390-103">Restore a StorSimple volume from a backup set</span></span>

## <a name="overview"></a><span data-ttu-id="fc390-104">概觀</span><span class="sxs-lookup"><span data-stu-id="fc390-104">Overview</span></span>

<span data-ttu-id="fc390-105">本教學課程說明在 StorSimple 8000 系列裝置上使用現有的備份組執行的還原作業。</span><span class="sxs-lookup"><span data-stu-id="fc390-105">This tutorial describes the restore operation performed on a StorSimple 8000 series device using an existing backup set.</span></span> <span data-ttu-id="fc390-106">使用 [備份類別目錄] 刀鋒視窗可從本機或雲端備份還原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-106">Use the **Backup catalog** blade to restore a volume from a local or cloud backup.</span></span> <span data-ttu-id="fc390-107">[備份類別目錄] 刀鋒視窗顯示在產生手動或自動備份時建立的所有備份組。</span><span class="sxs-lookup"><span data-stu-id="fc390-107">The **Backup catalog** blade displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="fc390-108">當資料在背景下載時，從備份組進行的還原作業會立即讓磁碟區連線。</span><span class="sxs-lookup"><span data-stu-id="fc390-108">The restore operation from a backup set brings the volume online immediately while data is downloaded in the background.</span></span>

<span data-ttu-id="fc390-109">啟動還原的一個替代方法是移至 [裝置] > [您的裝置] > [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="fc390-109">An alternate method to start restore is to go to **Devices > [Your device] > Volumes**.</span></span> <span data-ttu-id="fc390-110">在 [磁碟區] 刀鋒視窗中，選取磁碟區，以滑鼠右鍵按一下以叫用操作功能表，然後選取 [還原]。</span><span class="sxs-lookup"><span data-stu-id="fc390-110">In the **Volumes** blade, select a volume, right-click to invoke the context menu, and then select **Restore**.</span></span>

## <a name="before-you-restore"></a><span data-ttu-id="fc390-111">還原之前</span><span class="sxs-lookup"><span data-stu-id="fc390-111">Before you restore</span></span>

<span data-ttu-id="fc390-112">在開始還原之前，請先檢閱下列注意事項：</span><span class="sxs-lookup"><span data-stu-id="fc390-112">Before you start a restore, review the following caveats:</span></span>

* <span data-ttu-id="fc390-113">**必須使磁碟區離線** – 起始還原作業之前，同時讓主機和裝置上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="fc390-113">**You must take the volume offline** – Take the volume offline on both the host and the device before you initiate the restore operation.</span></span> <span data-ttu-id="fc390-114">雖然還原作業會自動使裝置上的磁碟區連線，但您必須手動讓主機上的裝置連線。</span><span class="sxs-lookup"><span data-stu-id="fc390-114">Although the restore operation automatically brings the volume online on the device, you must manually bring the device online on the host.</span></span> <span data-ttu-id="fc390-115">在裝置上的磁碟區連線之後，您就可以立即讓主機上的磁碟區連線。</span><span class="sxs-lookup"><span data-stu-id="fc390-115">You can bring the volume online on the host as soon as the volume is online on the device.</span></span> <span data-ttu-id="fc390-116">(不需要等到還原作業完成。)如需程序，請前往[使磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)。</span><span class="sxs-lookup"><span data-stu-id="fc390-116">(You do not need to wait until the restore operation is finished.) For procedures, go to [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).</span></span>

* <span data-ttu-id="fc390-117">**還原後的磁碟區類型** – 已刪除的磁碟區會根據快照集中的類型還原；亦即，固定在本機的磁碟機會還原為固定在本機的磁碟機，而分層磁碟機會還原為分層磁碟機。</span><span class="sxs-lookup"><span data-stu-id="fc390-117">**Volume type after restore** – Deleted volumes are restored based on the type in the snapshot; that is, volumes that were locally pinned are restored as locally pinned volumes and volumes that were tiered are restored as tiered volumes.</span></span>

    <span data-ttu-id="fc390-118">針對現有的磁碟區，磁碟機目前的使用類型會覆寫快照集中所還原的類型。</span><span class="sxs-lookup"><span data-stu-id="fc390-118">For existing volumes, the current usage type of the volume overrides the type that is stored in the snapshot.</span></span> <span data-ttu-id="fc390-119">例如，如果您從原本磁碟區類型為分層，而現在磁碟區類型為固定在本機 (因為已執行的轉換作業) 時所採取的快照集還原磁碟區，則磁碟區會還原成固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-119">For example, if you restore a volume from a snapshot that was taken when the volume type was tiered and that volume type is now locally pinned (due to a conversion operation that was performed), then the volume will be restored as a locally pinned volume.</span></span> <span data-ttu-id="fc390-120">同樣地，如果現有的固定在本機的磁碟區已擴充，且後續從過去磁碟區仍較小的舊快照集還原，還原的磁碟區將會保留目前擴充的大小。</span><span class="sxs-lookup"><span data-stu-id="fc390-120">Similarly, if an existing locally pinned volume was expanded and subsequently restored from an older snapshot taken when the volume was smaller, the restored volume will retain the current expanded size.</span></span>

    <span data-ttu-id="fc390-121">當磁碟區正在還原時，您無法從分層磁碟區轉換成固定在本機的磁碟區，或從固定在本機的磁碟區轉換成分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-121">You cannot convert a volume from a tiered volume to a locally pinned volume or from a locally pinned volume to a tiered volume while the volume is being restored.</span></span> <span data-ttu-id="fc390-122">請等候還原作業完成，您就能將磁碟區轉換為其他類型。</span><span class="sxs-lookup"><span data-stu-id="fc390-122">Wait until the restore operation is finished, and then you can convert the volume to another type.</span></span> <span data-ttu-id="fc390-123">如需轉換磁碟區的詳細資訊，請移至 [變更磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="fc390-123">For information about converting a volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span> 

* <span data-ttu-id="fc390-124">**磁碟區大小會反映在還原的磁碟區中** - 如果您要還原已刪除的固定在本機的磁碟區，這是很重要的考量 (因為要完整佈建固定在本機的磁碟區)。</span><span class="sxs-lookup"><span data-stu-id="fc390-124">**The volume size is reflected in the restored volume** – This is an important consideration if you are restoring a locally pinned volume that has been deleted (because locally pinned volumes are fully provisioned).</span></span> <span data-ttu-id="fc390-125">請確定您有足夠的空間，然後再嘗試還原之前已刪除的固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-125">Make sure that you have sufficient space before you attempt to restore a locally pinned volume that was previously deleted.</span></span>

* <span data-ttu-id="fc390-126">**正在還原時，您無法擴充磁碟區** – 等候還原作業完成，才能嘗試擴充磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-126">**You cannot expand a volume while it is being restored** – Wait until the restore operation is finished before you attempt to expand the volume.</span></span> <span data-ttu-id="fc390-127">如需有關擴充磁碟區的資訊，請移至 [修改磁碟區](storsimple-8000-manage-volumes-u2.md#modify-a-volume)。</span><span class="sxs-lookup"><span data-stu-id="fc390-127">For information about expanding a volume, go to [Modify a volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).</span></span>

* <span data-ttu-id="fc390-128">**還原本機磁碟區時，您可以執行備份** – 如需程序，請移至[使用 StorSimple 裝置管理員服務來管理備份原則](storsimple-8000-manage-backup-policies-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="fc390-128">**You can perform a backup while you restore a local volume** – For procedures go to [Use the StorSimple Device Manager service to manage backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>

* <span data-ttu-id="fc390-129">**可以取消還原作業** – 如果您取消還原工作，磁碟區將會回復到起始還原作業之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="fc390-129">**You can cancel a restore operation** – If you cancel the restore job, then the volume will be rolled back to the state that it was in before you initiated the restore operation.</span></span> <span data-ttu-id="fc390-130">如需程序，請移至 [取消工作](storsimple-8000-manage-jobs-u2.md#cancel-a-job)。</span><span class="sxs-lookup"><span data-stu-id="fc390-130">For procedures, go to [Cancel a job](storsimple-8000-manage-jobs-u2.md#cancel-a-job).</span></span>

## <a name="how-does-restore-work"></a><span data-ttu-id="fc390-131">還原的運作方式</span><span class="sxs-lookup"><span data-stu-id="fc390-131">How does restore work</span></span>

<span data-ttu-id="fc390-132">如果是執行 Update 4 或更新版本的裝置，就會實作熱度圖式還原。</span><span class="sxs-lookup"><span data-stu-id="fc390-132">For devices running Update 4 or later, a heatmap-based restore is implemented.</span></span> <span data-ttu-id="fc390-133">當存取資料的主機要求到達裝置時，即會追蹤這些要求並建立熱度圖。</span><span class="sxs-lookup"><span data-stu-id="fc390-133">As the host requests to access data reach the device, these requests are tracked and a heatmap is created.</span></span> <span data-ttu-id="fc390-134">高要求率會產生具有更高熱度的資料區塊，而較低的要求率會轉譯為熱度較低的區塊。</span><span class="sxs-lookup"><span data-stu-id="fc390-134">High request rate results in data chunks with higher heat whereas lower request rate translates to chunks with lower heat.</span></span> <span data-ttu-id="fc390-135">您必須存取資料至少兩次，才能將其標示為「熱」。</span><span class="sxs-lookup"><span data-stu-id="fc390-135">You must access the data atleast twice to be marked as _hot_.</span></span> <span data-ttu-id="fc390-136">已修改的檔案也會標示為「熱」。</span><span class="sxs-lookup"><span data-stu-id="fc390-136">A file that is modified is also marked as _hot_.</span></span> <span data-ttu-id="fc390-137">一旦您起始還原之後，接著會根據熱度圖進行資料的主動式水化。</span><span class="sxs-lookup"><span data-stu-id="fc390-137">Once you initiate the restore, then proactive hydration of data occurs based on the heatmap.</span></span> <span data-ttu-id="fc390-138">如果版本早於 Update 4，就只會在還原期間根據存取下載資料。</span><span class="sxs-lookup"><span data-stu-id="fc390-138">For versions earlier than Update 4, the data is downloaded during restore based on access only.</span></span>

<span data-ttu-id="fc390-139">下列注意事項適用於熱度圖式還原：</span><span class="sxs-lookup"><span data-stu-id="fc390-139">The following caveats apply to heatmap-based restores:</span></span>

* <span data-ttu-id="fc390-140">熱度圖追蹤只適用於階層式磁碟區，不支援固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-140">Heatmap tracking is enabled only for tiered volumes and locally pinned volumes are not supported.</span></span>

* <span data-ttu-id="fc390-141">將磁碟區複製到另一個裝置時，不支援熱度圖式還原。</span><span class="sxs-lookup"><span data-stu-id="fc390-141">Heatmap-based restore is not supported when cloning a volume to another device.</span></span> 

* <span data-ttu-id="fc390-142">如果有就地還原且裝置上目前有要還原之磁碟區的本機快照集，則我們不會解除凍結 (因為資料已經可在本機使用)。</span><span class="sxs-lookup"><span data-stu-id="fc390-142">If there is an in-place restore and a local snapshot for the volume to be restored exists on the device, then we do not rehydrate (as data is already available locally).</span></span> 

* <span data-ttu-id="fc390-143">根據預設，當您還原時，會起始解除凍結作業，以根據熱度圖主動解除凍結資料。</span><span class="sxs-lookup"><span data-stu-id="fc390-143">By default, when you restore, the rehydration jobs are initiated that proactively rehydrate data based on the heatmap.</span></span> 

<span data-ttu-id="fc390-144">在 Update 4 中，Windows PowerShell Cmdlet 可用來查詢執行中的解除凍結作業、取消解除凍結作業，以及取得解除凍結作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="fc390-144">In Update 4, Windows PowerShell cmdlets can be used to query running rehydration jobs, cancel a rehydration job, and get the status of the rehydration job.</span></span>

* <span data-ttu-id="fc390-145">`Get-HcsRehydrationJob` -此 Cmdlet 會取得解除凍結作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="fc390-145">`Get-HcsRehydrationJob` - This cmdlet gets the status of the rehydration job.</span></span> <span data-ttu-id="fc390-146">單一解除凍結作業會針對某一個磁碟區來觸發。</span><span class="sxs-lookup"><span data-stu-id="fc390-146">A single rehydration job is triggered for one volume.</span></span>

* <span data-ttu-id="fc390-147">`Set-HcsRehydrationJob` - 此 Cmdlet 可讓您在解除凍結正在進行時暫停、停止、繼續執行解除凍結作業。</span><span class="sxs-lookup"><span data-stu-id="fc390-147">`Set-HcsRehydrationJob` - This cmdlet allows you to pause, stop, resume the rehydration job, when the rehydration is in progress.</span></span>

<span data-ttu-id="fc390-148">如需解除凍結 Cmdlet 的詳細資訊，請移至[適用於 StorSimple 的 Windows PowerShell Cmdlet 參考](https://technet.microsoft.com/library/dn688168.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fc390-148">For more information on rehydration cmdlets, go to [Windows PowerShell cmdlet reference for StorSimple](https://technet.microsoft.com/library/dn688168.aspx).</span></span>

<span data-ttu-id="fc390-149">透過自動解除凍結功能，通常可預期較高的暫時性讀取效能。</span><span class="sxs-lookup"><span data-stu-id="fc390-149">With automatic rehdyration, typically higher transient read performance is expected.</span></span> <span data-ttu-id="fc390-150">改進的實際範圍取決於各種因素，例如存取模式、資料變換及資料類型。</span><span class="sxs-lookup"><span data-stu-id="fc390-150">The actual magniutde of improvements depends on various factors such as access pattern, data churn, and data type.</span></span> 

<span data-ttu-id="fc390-151">若要取消解除凍結作業，您可以使用 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fc390-151">To cancel a rehydration job, you can use the PowerShell cmdlet.</span></span> <span data-ttu-id="fc390-152">如果您希望針對所有未來的還原作業永久停用解除凍結作業，請[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="fc390-152">If you wish to permanently disable rehydration jobs for all the future restores, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="fc390-153">如何使用備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="fc390-153">How to use the backup catalog</span></span>

<span data-ttu-id="fc390-154">[備份類別目錄] 刀鋒視窗提供查詢，可協助您縮小備份組選取範圍。</span><span class="sxs-lookup"><span data-stu-id="fc390-154">The **Backup Catalog** blade provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="fc390-155">您可以篩選根據下列參數擷取的備份組：</span><span class="sxs-lookup"><span data-stu-id="fc390-155">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="fc390-156">**時間範圍** – 建立備份組的日期和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="fc390-156">**Time range** – The date and time range when the backup set was created.</span></span>
* <span data-ttu-id="fc390-157">**裝置** - 建立備份組所在的裝置。</span><span class="sxs-lookup"><span data-stu-id="fc390-157">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="fc390-158">**備份原則**或**磁碟區** – 與此備份組相關聯的備份原則或磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-158">**Backup policy** or **Volume** – The backup policy or volume associated with this backup set.</span></span>

<span data-ttu-id="fc390-159">接著會根據下列屬性，將篩選的備份組列表顯示：</span><span class="sxs-lookup"><span data-stu-id="fc390-159">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="fc390-160">**名稱** - 與備份組相關聯的備份原則或磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc390-160">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="fc390-161">**類型** - 備份組可以是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="fc390-161">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="fc390-162">本機快照是本機儲存於裝置上的所有磁碟區資料備份，而雲端快照是指位於雲端的磁碟區資料備份。</span><span class="sxs-lookup"><span data-stu-id="fc390-162">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="fc390-163">本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。</span><span class="sxs-lookup"><span data-stu-id="fc390-163">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="fc390-164">**大小** - 備份組的實際大小。</span><span class="sxs-lookup"><span data-stu-id="fc390-164">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="fc390-165">**建立日期** - 建立備份的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="fc390-165">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="fc390-166">**磁碟區** - 與備份組相關聯的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="fc390-166">**Volumes** - The number of volumes associated with the backup set.</span></span>
* <span data-ttu-id="fc390-167">**起始方式** - 備份可根據排程自動起始，或由使用者手動起始。</span><span class="sxs-lookup"><span data-stu-id="fc390-167">**Initiated** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="fc390-168">(您可以使用備份原則來排程備份。</span><span class="sxs-lookup"><span data-stu-id="fc390-168">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="fc390-169">或者，可以使用 [進行備份] 選項來進行互動式或隨選備份。)</span><span class="sxs-lookup"><span data-stu-id="fc390-169">Alternatively, you can use the **Take backup** option to take an interactive or on-demand backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="fc390-170">如何從備份還原您的 StorSimple 磁碟區</span><span class="sxs-lookup"><span data-stu-id="fc390-170">How to restore your StorSimple volume from a backup</span></span>

<span data-ttu-id="fc390-171">您可以使用 [備份類別目錄] 刀鋒視窗，從特定的備份還原 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-171">You can use the **Backup Catalog** blade to restore your StorSimple volume from a specific backup.</span></span> <span data-ttu-id="fc390-172">不過，請記住，還原磁碟區會將磁碟區的狀態還原為其在取得備份時的狀態。</span><span class="sxs-lookup"><span data-stu-id="fc390-172">Keep in mind, however, that restoring a volume will revert the volume to the state it was in when the backup was taken.</span></span> <span data-ttu-id="fc390-173">在備份作業之後新增的所有資料都將遺失。</span><span class="sxs-lookup"><span data-stu-id="fc390-173">Any data that was added after the backup operation will be lost.</span></span>

> [!WARNING]
> <span data-ttu-id="fc390-174">從備份還原將從備份取代現有的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-174">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="fc390-175">這可能會造成在取得備份之後寫入的所有資料遺失。</span><span class="sxs-lookup"><span data-stu-id="fc390-175">This may cause the loss of any data that was written after the backup was taken.</span></span>


### <a name="to-restore-your-volume"></a><span data-ttu-id="fc390-176">還原您的磁碟區</span><span class="sxs-lookup"><span data-stu-id="fc390-176">To restore your volume</span></span>
1. <span data-ttu-id="fc390-177">移至 StorSimple 裝置管理員服務，然後按一下 [備份類別目錄]。</span><span class="sxs-lookup"><span data-stu-id="fc390-177">Go to your StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="fc390-178">選取備份組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fc390-178">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="fc390-179">指定時間範圍。</span><span class="sxs-lookup"><span data-stu-id="fc390-179">Specify the time range.</span></span>
   2. <span data-ttu-id="fc390-180">選取適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="fc390-180">Select the appropriate device.</span></span>
   3. <span data-ttu-id="fc390-181">在下拉式清單中，針對要選取的備份選擇磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="fc390-181">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   4. <span data-ttu-id="fc390-182">按一下 [套用] 以執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="fc390-182">Click **Apply** to execute this query.</span></span>

    <span data-ttu-id="fc390-183">與選取的磁碟區或備份原則相關聯的備份應該會出現在備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="fc390-183">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
   
    ![備份組清單](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. <span data-ttu-id="fc390-185">展開備份組以檢視相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fc390-185">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="fc390-186">您必須先在主機和裝置上將這些磁碟區離線，才能還原它們。</span><span class="sxs-lookup"><span data-stu-id="fc390-186">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="fc390-187">存取您裝置上 [磁碟區] 刀鋒視窗上的磁碟區，然後依照[讓磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)中的步驟來讓它們離線。</span><span class="sxs-lookup"><span data-stu-id="fc390-187">Access the volumes on the **Volumes** blade of your device, and then follow the steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) to take them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="fc390-188">確定您已先讓主機上的磁碟區離線，然後再讓裝置上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="fc390-188">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="fc390-189">如果您並未讓主機上的磁碟區離線，可能會導致資料損毀。</span><span class="sxs-lookup"><span data-stu-id="fc390-189">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   
4. <span data-ttu-id="fc390-190">瀏覽回到 [備份類別目錄]  索引標籤，並選取備份組。</span><span class="sxs-lookup"><span data-stu-id="fc390-190">Navigate back to the **Backup Catalog** tab and select a backup set.</span></span> <span data-ttu-id="fc390-191">以滑鼠右鍵按一下，然後從操作功能表中選取 [還原]。</span><span class="sxs-lookup"><span data-stu-id="fc390-191">Right-click and then from the context menu, select **Restore**.</span></span>

    ![備份組清單](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. <span data-ttu-id="fc390-193">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="fc390-193">You will be prompted for confirmation.</span></span> <span data-ttu-id="fc390-194">檢閱還原資訊，然後選取 [確認] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="fc390-194">Review the restore information, and then select the confirmation check box.</span></span>
   
    ![確認電子郵件](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  <span data-ttu-id="fc390-196">按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="fc390-196">Click **Restore**.</span></span> <span data-ttu-id="fc390-197">這將會起始還原工作，而您可以存取 [工作] 頁面來檢視。</span><span class="sxs-lookup"><span data-stu-id="fc390-197">This initiates a restore job that you can view by accessing the **Jobs** page.</span></span>

    ![確認電子郵件](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. <span data-ttu-id="fc390-199">還原完成之後，請確認磁碟區的內容已由備份的磁碟區所取代。</span><span class="sxs-lookup"><span data-stu-id="fc390-199">After the restore is complete, verify that the contents of your volumes are replaced by volumes from the backup.</span></span>


## <a name="if-the-restore-fails"></a><span data-ttu-id="fc390-200">如果還原失敗</span><span class="sxs-lookup"><span data-stu-id="fc390-200">If the restore fails</span></span>

<span data-ttu-id="fc390-201">如果還原作業因為任何原因而失敗，您會收到警示。</span><span class="sxs-lookup"><span data-stu-id="fc390-201">You will receive an alert if the restore operation fails for any reason.</span></span> <span data-ttu-id="fc390-202">如果發生這種情況，請重新整理備份清單，以確認備份仍然有效。</span><span class="sxs-lookup"><span data-stu-id="fc390-202">If this occurs, refresh the backup list to verify that the backup is still valid.</span></span> <span data-ttu-id="fc390-203">如果備份有效，且您是從雲端還原，則連線問題可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="fc390-203">If the backup is valid and you are restoring from the cloud, then connectivity issues might be causing the problem.</span></span>

<span data-ttu-id="fc390-204">若要完成還原作業，請使主機上的磁碟區離線，然後重試還原作業。</span><span class="sxs-lookup"><span data-stu-id="fc390-204">To complete the restore operation, take the volume offline on the host and retry the restore operation.</span></span> <span data-ttu-id="fc390-205">請注意，在還原程序期間所執行的磁碟區資料修改將會遺失。</span><span class="sxs-lookup"><span data-stu-id="fc390-205">Note that any modifications to the volume data that were performed during the restore process will be lost.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc390-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc390-206">Next steps</span></span>
* <span data-ttu-id="fc390-207">了解如何 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="fc390-207">Learn how to [Manage StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="fc390-208">了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="fc390-208">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

