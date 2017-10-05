---
title: "複製 StorSimple 8000 系列磁碟區 | Microsoft Docs"
description: "說明不同的複製類型以及使用時機，並說明如何使用備份組來複製個別磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 2b627250df62bbe3299869ef3812947afbb8f29f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume-update-2"></a><span data-ttu-id="581ca-103">使用 StorSimple Manager 服務來複製磁碟區 (Update 2)</span><span class="sxs-lookup"><span data-stu-id="581ca-103">Use the StorSimple Manager service to clone a volume (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="581ca-104">概觀</span><span class="sxs-lookup"><span data-stu-id="581ca-104">Overview</span></span>
<span data-ttu-id="581ca-105">StorSimple Manager 服務 [備份類別目錄]  頁面會顯示在進行手動或自動備份時所建立的所有備份組。</span><span class="sxs-lookup"><span data-stu-id="581ca-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="581ca-106">您可以使用此頁面來列出備份原則或磁碟區的所有備份、選取或刪除備份，或是使用備份來還原或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![備份類別目錄頁面](./media/storsimple-clone-volume-u2/backupCatalog.png)  

<span data-ttu-id="581ca-108">本教學課程說明如何使用備份組來複製個別磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="581ca-109">它也會說明「暫時性」與「永久」複製之間的差異。</span><span class="sxs-lookup"><span data-stu-id="581ca-109">It also explains the difference between *transient* and *permanent* clones.</span></span>

> [!NOTE]
> <span data-ttu-id="581ca-110">固定在本機的磁碟區將會複製為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-110">A locally pinned volume will be cloned as a tiered volume.</span></span> <span data-ttu-id="581ca-111">如果您需要將複製的磁碟區固定在本機，可以在複製作業成功完成之後，再將複製品轉換為固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-111">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="581ca-112">如需將分層磁碟區轉換為固定在本機的磁碟區的詳細資訊，請移至 [變更磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="581ca-112">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
> 
> <span data-ttu-id="581ca-113">如果您嘗試在複製之後 (當其仍為暫時性複製品) 立即將分層磁碟區轉換為固定在本機的磁碟區，則轉換會失敗並出現下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="581ca-113">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion will fail with the following error message:</span></span>
> 
> `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.` 
> 
> <span data-ttu-id="581ca-114">只有在您複製到不同裝置時才會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="581ca-114">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="581ca-115">先將暫時性複製品轉換為永久複製品，即可成功將磁碟區轉換為固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-115">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="581ca-116">若要將暫時性複製品轉換為永久複製品，請拍下其雲端快照。</span><span class="sxs-lookup"><span data-stu-id="581ca-116">To convert the transient clone to a permanent clone, take a cloud snapshot of it.</span></span>
> 
> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="581ca-117">建立磁碟區複製</span><span class="sxs-lookup"><span data-stu-id="581ca-117">Create a clone of a volume</span></span>
<span data-ttu-id="581ca-118">您可以使用本機或雲端快照，在相同的裝置、另一個裝置，甚或虛擬機器上建立複製品。</span><span class="sxs-lookup"><span data-stu-id="581ca-118">You can create a clone on the same device, another device, or even a virtual machine by using a local or cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="581ca-119">若要複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="581ca-119">To clone a volume</span></span>
1. <span data-ttu-id="581ca-120">在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤，然後選取備份組。</span><span class="sxs-lookup"><span data-stu-id="581ca-120">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="581ca-121">展開備份組以檢視相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-121">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="581ca-122">從備份組中按一下並選取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-122">Click and select a volume from the backup set.</span></span>
   
     ![複製磁碟區](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. <span data-ttu-id="581ca-124">按一下 [複製]  ，以開始複製選取的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-124">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="581ca-125">在 [複製磁碟區精靈] 的 [指定名稱和位置] 下：</span><span class="sxs-lookup"><span data-stu-id="581ca-125">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="581ca-126">識別目標裝置。</span><span class="sxs-lookup"><span data-stu-id="581ca-126">Identify a target device.</span></span> <span data-ttu-id="581ca-127">這是即將建立複製的位置。</span><span class="sxs-lookup"><span data-stu-id="581ca-127">This is the location where the clone will be created.</span></span> <span data-ttu-id="581ca-128">您可以選擇相同的裝置，或指定另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="581ca-128">You can choose the same device or specify another device.</span></span> <span data-ttu-id="581ca-129">如果您選擇與其他雲端服務提供者相關的磁碟區 (非 Azure)，目標裝置的下拉式清單將只會顯示實體裝置。</span><span class="sxs-lookup"><span data-stu-id="581ca-129">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="581ca-130">您無法在虛擬裝置上複製與其他雲端服務提供者相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-130">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="581ca-131">確定要複製的容量小於目標裝置中可用的容量。</span><span class="sxs-lookup"><span data-stu-id="581ca-131">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="581ca-132">為複製指定唯一的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="581ca-132">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="581ca-133">此名稱必須包含 3 到 127 個字元。</span><span class="sxs-lookup"><span data-stu-id="581ca-133">The name must contain between 3 and 127 characters.</span></span> 
      
      > [!NOTE]
      > <span data-ttu-id="581ca-134">即使您複製了本機釘選磁碟區，[將磁碟區複製為] 欄位仍然會**分層**。</span><span class="sxs-lookup"><span data-stu-id="581ca-134">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="581ca-135">您無法變更此設定，但如果您需要在本機釘選複製的磁碟區，您可以在成功建立複製之後，將複製轉換到本機釘選的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-135">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="581ca-136">如需將分層磁碟區轉換為固定在本機的磁碟區的詳細資訊，請移至 [變更磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="581ca-136">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
      > 
      > 
      
        ![複製精靈 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. <span data-ttu-id="581ca-138">按一下箭頭圖示 </span><span class="sxs-lookup"><span data-stu-id="581ca-138">Click the arrow icon</span></span> ![arrow-icon](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) <span data-ttu-id="581ca-140">，繼續前往下一頁。</span><span class="sxs-lookup"><span data-stu-id="581ca-140">to proceed to the next page.</span></span>
5. <span data-ttu-id="581ca-141">在 [指定可以使用此磁碟區的主機] 下：</span><span class="sxs-lookup"><span data-stu-id="581ca-141">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="581ca-142">指定該複製的存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="581ca-142">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="581ca-143">您可以加入新的 ACR，或從現有清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="581ca-143">You can add a new ACR or choose from the existing list.</span></span>
      
        ![複製精靈 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. <span data-ttu-id="581ca-145">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="581ca-145">Click the check icon</span></span> ![核取圖示](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)<span data-ttu-id="581ca-147">完成操作。</span><span class="sxs-lookup"><span data-stu-id="581ca-147">to complete the operation.</span></span>
6. <span data-ttu-id="581ca-148">複製工作隨即起始並在成功建立複製時通知您。</span><span class="sxs-lookup"><span data-stu-id="581ca-148">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="581ca-149">按一下 [檢視工作]，在 [工作] 頁面上監視複製工作。</span><span class="sxs-lookup"><span data-stu-id="581ca-149">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span> <span data-ttu-id="581ca-150">複製作業完成時，您會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="581ca-150">You will see the following message when the clone job is finished:</span></span>
   
    ![複製訊息](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. <span data-ttu-id="581ca-152">複製工作完成後：</span><span class="sxs-lookup"><span data-stu-id="581ca-152">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="581ca-153">移至 [裝置] 頁面，然後選取 [磁碟區容器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="581ca-153">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="581ca-154">選取與複製的來源磁碟區相關聯的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="581ca-154">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="581ca-155">您應該會在磁碟區清單中看到剛才建立的複製。</span><span class="sxs-lookup"><span data-stu-id="581ca-155">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="581ca-156">複製的磁碟區上會自動停用監視和預設備份。</span><span class="sxs-lookup"><span data-stu-id="581ca-156">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="581ca-157">以這種方式建立的複製就是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="581ca-157">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="581ca-158">如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。</span><span class="sxs-lookup"><span data-stu-id="581ca-158">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="581ca-159">此複製現在是一般的磁碟區，可在磁碟區進行的任何操作都能在此複製進行。</span><span class="sxs-lookup"><span data-stu-id="581ca-159">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="581ca-160">您必須設定此磁碟區以進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="581ca-160">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="581ca-161">暫時性與永久複製</span><span class="sxs-lookup"><span data-stu-id="581ca-161">Transient vs. permanent clones</span></span>
<span data-ttu-id="581ca-162">只有在您複製到不同裝置時才會建立暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="581ca-162">Transient clones are created only when you are cloning to a different device.</span></span> <span data-ttu-id="581ca-163">您可以從備份組複製特定磁碟區到受 StorSimple Manager 管理的不同裝置。</span><span class="sxs-lookup"><span data-stu-id="581ca-163">You can clone a specific volume from a backup set to a different device managed by the StorSimple Manager.</span></span> <span data-ttu-id="581ca-164">暫時性複製會有原始磁碟區中資料的參考，並使用該資料在目標裝置本機上讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="581ca-164">The transient clone will have references to the data in the original volume and will use that data to read and write locally on the target device.</span></span> 

<span data-ttu-id="581ca-165">在建立暫時性複製的雲端快照之後，產生的複製就是「永久」  複製。</span><span class="sxs-lookup"><span data-stu-id="581ca-165">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="581ca-166">在此程序中，會在雲端建立資料複本，而複製此資料的時機則由資料大小和 Azure 的延遲來決定 (這是 Azure 對 Azure 複製)。</span><span class="sxs-lookup"><span data-stu-id="581ca-166">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="581ca-167">此程序可能需要數天至數週。</span><span class="sxs-lookup"><span data-stu-id="581ca-167">This process can take days to weeks.</span></span> <span data-ttu-id="581ca-168">暫時性複製會透過這個方式成為永久性複製，且沒有對所複製原始磁碟區資料的任何參考。</span><span class="sxs-lookup"><span data-stu-id="581ca-168">The transient clone becomes a permanent clone this way and doesn’t have any references to the original volume data that it was cloned from.</span></span> 

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="581ca-169">暫時性複製與永久複製的案例</span><span class="sxs-lookup"><span data-stu-id="581ca-169">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="581ca-170">下列各節將說明可使用暫時性複製與永久複製的範例情況。</span><span class="sxs-lookup"><span data-stu-id="581ca-170">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="581ca-171">使用暫時性複製復原項目層級</span><span class="sxs-lookup"><span data-stu-id="581ca-171">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="581ca-172">您要復原過去一年的 Microsoft PowerPoint 簡報檔案。</span><span class="sxs-lookup"><span data-stu-id="581ca-172">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="581ca-173">IT 系統管理員辨識該時間範圍內的特定備份，然後篩選磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-173">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="581ca-174">系統管理員接著再複製磁碟區，找出您要找的檔案再提供給您。</span><span class="sxs-lookup"><span data-stu-id="581ca-174">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="581ca-175">在此案例中，使用的是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="581ca-175">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="581ca-176">![提供的影片](./media/storsimple-clone-volume-u2/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="581ca-176">![Video available](./media/storsimple-clone-volume-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="581ca-177">若要觀看影片示範如何使用 StorSimple 的複製和還原功能來復原已刪除的檔案，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="581ca-177">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="581ca-178">利用永久複製在實際執行環境中進行測試</span><span class="sxs-lookup"><span data-stu-id="581ca-178">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="581ca-179">您需要確認生產環境中的測試錯誤。</span><span class="sxs-lookup"><span data-stu-id="581ca-179">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="581ca-180">您在生產環境中建立磁碟區的複製，並採用這個複製的雲端快照來建立獨立的複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="581ca-180">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="581ca-181">在此案例中，使用的是永久複製。</span><span class="sxs-lookup"><span data-stu-id="581ca-181">In this scenario, a permanent clone is used.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="581ca-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="581ca-182">Next steps</span></span>
* <span data-ttu-id="581ca-183">了解如何 [從備份組還原 StorSimple 磁碟區](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="581ca-183">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="581ca-184">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="581ca-184">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

