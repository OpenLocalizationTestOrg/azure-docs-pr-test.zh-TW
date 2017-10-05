---
title: "複製 StorSimple 磁碟區 | Microsoft Docs"
description: "說明不同的複製類型以及使用時機，並說明如何使用備份組來複製個別磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 8f1936fac543f559a44ad0f9c35b30d1a92dce68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a><span data-ttu-id="5e996-103">使用 StorSimple Manager 服務來複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="5e996-103">Use the StorSimple Manager service to clone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="5e996-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5e996-104">Overview</span></span>
<span data-ttu-id="5e996-105">StorSimple Manager 服務 [備份類別目錄]  頁面會顯示在進行手動或自動備份時所建立的所有備份組。</span><span class="sxs-lookup"><span data-stu-id="5e996-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="5e996-106">您可以使用此頁面來列出備份原則或磁碟區的所有備份、選取或刪除備份，或是使用備份來還原或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![備份類別目錄頁面](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="5e996-108">本教學課程說明如何使用備份組來複製個別磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="5e996-109">它也會說明「暫時性」與「永久」複製之間的差異。</span><span class="sxs-lookup"><span data-stu-id="5e996-109">It also explains the difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="5e996-110">建立磁碟區複製</span><span class="sxs-lookup"><span data-stu-id="5e996-110">Create a clone of a volume</span></span>
<span data-ttu-id="5e996-111">您可以使用本機或雲端快照，在相同的裝置、 另一個裝置或甚至虛擬機器上建立複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="5e996-112">若要複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="5e996-112">To clone a volume</span></span>
1. <span data-ttu-id="5e996-113">在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤，然後選取備份組。</span><span class="sxs-lookup"><span data-stu-id="5e996-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="5e996-114">展開備份組以檢視相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-114">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="5e996-115">從備份組中按一下並選取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-115">Click and select a volume from the backup set.</span></span>
   
     ![複製磁碟區](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="5e996-117">按一下 [複製]  ，以開始複製選取的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-117">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="5e996-118">在 [複製磁碟區精靈] 的 [指定名稱和位置] 下：</span><span class="sxs-lookup"><span data-stu-id="5e996-118">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="5e996-119">識別目標裝置。</span><span class="sxs-lookup"><span data-stu-id="5e996-119">Identify a target device.</span></span> <span data-ttu-id="5e996-120">這是即將建立複製的位置。</span><span class="sxs-lookup"><span data-stu-id="5e996-120">This is the location where the clone will be created.</span></span> <span data-ttu-id="5e996-121">您可以選擇相同的裝置，或指定另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="5e996-121">You can choose the same device or specify another device.</span></span> <span data-ttu-id="5e996-122">如果您選擇與其他雲端服務提供者相關的磁碟區 (非 Azure)，目標裝置的下拉式清單將只會顯示實體裝置。</span><span class="sxs-lookup"><span data-stu-id="5e996-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="5e996-123">您無法在虛擬裝置上複製與其他雲端服務提供者相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="5e996-124">確定要複製的容量小於目標裝置中可用的容量。</span><span class="sxs-lookup"><span data-stu-id="5e996-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="5e996-125">為複製指定唯一的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="5e996-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="5e996-126">此名稱必須包含 3 到 127 個字元。</span><span class="sxs-lookup"><span data-stu-id="5e996-126">The name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="5e996-127">按一下箭頭圖示 </span><span class="sxs-lookup"><span data-stu-id="5e996-127">Click the arrow icon</span></span> ![arrow-icon](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="5e996-129">，繼續前往下一頁。</span><span class="sxs-lookup"><span data-stu-id="5e996-129">to proceed to the next page.</span></span>
5. <span data-ttu-id="5e996-130">在 [指定可以使用此磁碟區的主機] 下：</span><span class="sxs-lookup"><span data-stu-id="5e996-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="5e996-131">指定該複製的存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="5e996-131">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="5e996-132">您可以加入新的 ACR，或從現有清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="5e996-132">You can add a new ACR or choose from the existing list.</span></span>
   2. <span data-ttu-id="5e996-133">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="5e996-133">Click the check icon</span></span> ![核取圖示](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="5e996-135">完成操作。</span><span class="sxs-lookup"><span data-stu-id="5e996-135">to complete the operation.</span></span>
6. <span data-ttu-id="5e996-136">複製工作隨即起始並在成功建立複製時通知您。</span><span class="sxs-lookup"><span data-stu-id="5e996-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="5e996-137">按一下 [檢視工作]，在 [工作] 頁面上監視複製工作。</span><span class="sxs-lookup"><span data-stu-id="5e996-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span>
7. <span data-ttu-id="5e996-138">複製工作完成後：</span><span class="sxs-lookup"><span data-stu-id="5e996-138">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="5e996-139">移至 [裝置] 頁面，然後選取 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5e996-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="5e996-140">選取與複製的來源磁碟區相關聯的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="5e996-140">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="5e996-141">您應該會在磁碟區清單中看到剛才建立的複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-141">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="5e996-142">複製的磁碟區上會自動停用監視和預設備份。</span><span class="sxs-lookup"><span data-stu-id="5e996-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="5e996-143">以這種方式建立的複製就是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="5e996-144">如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。</span><span class="sxs-lookup"><span data-stu-id="5e996-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="5e996-145">此複製現在是一般的磁碟區，可在磁碟區進行的任何操作都能在此複製進行。</span><span class="sxs-lookup"><span data-stu-id="5e996-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="5e996-146">您必須設定此磁碟區以進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="5e996-146">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="5e996-147">暫時性與永久複製</span><span class="sxs-lookup"><span data-stu-id="5e996-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="5e996-148">只有在您複製到不同裝置時才會建立暫時性和永久複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-148">Transient and permanent clones are created only when you are cloning on to a different device.</span></span> <span data-ttu-id="5e996-149">您可以從備份組複製特定磁碟區到不同裝置。</span><span class="sxs-lookup"><span data-stu-id="5e996-149">You can clone a specific volume from a backup set to a different device.</span></span> <span data-ttu-id="5e996-150">以這種方式建立的複製就是「暫時性」  複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="5e996-151">暫時性複製會有原始磁碟區的參考，並在本機寫入時使用該磁碟區來讀取。</span><span class="sxs-lookup"><span data-stu-id="5e996-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span></span> 

<span data-ttu-id="5e996-152">在建立暫時性複製的雲端快照之後，產生的複製就是「永久」  複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="5e996-153">永久複製獨立且沒有所複製原始磁碟區的任何參考。</span><span class="sxs-lookup"><span data-stu-id="5e996-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="5e996-154">暫時性複製與永久複製的案例</span><span class="sxs-lookup"><span data-stu-id="5e996-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="5e996-155">下列各節將說明可使用暫時性複製與永久複製的範例情況。</span><span class="sxs-lookup"><span data-stu-id="5e996-155">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="5e996-156">使用暫時性複製復原項目層級</span><span class="sxs-lookup"><span data-stu-id="5e996-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="5e996-157">您要復原過去一年的 Microsoft PowerPoint 簡報檔案。</span><span class="sxs-lookup"><span data-stu-id="5e996-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="5e996-158">IT 系統管理員辨識該時間範圍內的特定備份，然後篩選磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5e996-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="5e996-159">系統管理員接著再複製磁碟區，找出您要找的檔案再提供給您。</span><span class="sxs-lookup"><span data-stu-id="5e996-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="5e996-160">在此案例中，使用的是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="5e996-161">![提供的影片](./media/storsimple-clone-volume/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="5e996-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="5e996-162">若要觀看影片示範如何使用 StorSimple 的複製和還原功能來復原已刪除的檔案，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="5e996-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="5e996-163">利用永久複製在實際執行環境中進行測試</span><span class="sxs-lookup"><span data-stu-id="5e996-163">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="5e996-164">您需要確認生產環境中的測試錯誤。</span><span class="sxs-lookup"><span data-stu-id="5e996-164">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="5e996-165">您要使用複製的雲端快照，在生產環境中建立磁碟區的複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="5e996-166">複製的磁碟區現在是獨立的。</span><span class="sxs-lookup"><span data-stu-id="5e996-166">The cloned volume is now independent.</span></span> <span data-ttu-id="5e996-167">在此案例中，使用的是永久複製。</span><span class="sxs-lookup"><span data-stu-id="5e996-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e996-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e996-168">Next steps</span></span>
* <span data-ttu-id="5e996-169">了解如何 [從備份組還原 StorSimple 磁碟區](storsimple-restore-from-backup-set.md)。</span><span class="sxs-lookup"><span data-stu-id="5e996-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="5e996-170">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="5e996-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

