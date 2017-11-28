---
title: "aaaClone StorSimple 8000 系列的磁碟區 |Microsoft 文件"
description: "描述 hello 複製不同類型和當 toouse 它們，並說明如何使用備份組 tooclone 個別磁碟區。"
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
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a><span data-ttu-id="56d09-103">使用 hello StorSimple Manager 服務 tooclone (Update 2) 的磁碟區</span><span class="sxs-lookup"><span data-stu-id="56d09-103">Use hello StorSimple Manager service tooclone a volume (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="56d09-104">概觀</span><span class="sxs-lookup"><span data-stu-id="56d09-104">Overview</span></span>
<span data-ttu-id="56d09-105">StorSimple Manager 服務的 hello**備份類別目錄**頁面會顯示所有 hello 的備份組時手動或自動備份所建立的。</span><span class="sxs-lookup"><span data-stu-id="56d09-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="56d09-106">您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

![備份類別目錄頁面](./media/storsimple-clone-volume-u2/backupCatalog.png)  

<span data-ttu-id="56d09-108">本教學課程說明如何使用備份組 tooclone 個別磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-108">This tutorial describes how you can use a backup set tooclone an individual volume.</span></span> <span data-ttu-id="56d09-109">它也會說明 hello 差異*暫時性*和*永久*複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-109">It also explains hello difference between *transient* and *permanent* clones.</span></span>

> [!NOTE]
> <span data-ttu-id="56d09-110">固定在本機的磁碟區將會複製為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-110">A locally pinned volume will be cloned as a tiered volume.</span></span> <span data-ttu-id="56d09-111">如果您需要 hello 固定在本機複製的磁碟區 toobe，您可以在 hello 複製作業成功完成之後，轉換 hello 複製 tooa 固定在本機磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-111">If you need hello cloned volume toobe locally pinned, you can convert hello clone tooa locally pinned volume after hello clone operation is successfully completed.</span></span> <span data-ttu-id="56d09-112">資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="56d09-112">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
> 
> <span data-ttu-id="56d09-113">如果您嘗試複製的磁碟區，從階層式 toolocally 釘選之後立即複製 （當它仍然是暫時性複本） 的 tooconvert，hello 轉換會失敗並 hello 下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="56d09-113">If you try tooconvert a cloned volume from tiered toolocally pinned immediately after cloning (when it is still a transient clone), hello conversion will fail with hello following error message:</span></span>
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> <span data-ttu-id="56d09-114">只有當您正在複製 tooa 不同裝置上，會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="56d09-114">This error is received only if you are cloning on tooa different device.</span></span> <span data-ttu-id="56d09-115">您可以成功地轉換 hello 磁碟區 toolocally 釘選，如果您先轉換 hello 暫時性複本 tooa 永久性複本。</span><span class="sxs-lookup"><span data-stu-id="56d09-115">You can successfully convert hello volume toolocally pinned if you first convert hello transient clone tooa permanent clone.</span></span> <span data-ttu-id="56d09-116">tooconvert hello 暫時性複本 tooa 永久複製，建立它的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="56d09-116">tooconvert hello transient clone tooa permanent clone, take a cloud snapshot of it.</span></span>
> 
> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="56d09-117">建立磁碟區複製</span><span class="sxs-lookup"><span data-stu-id="56d09-117">Create a clone of a volume</span></span>
<span data-ttu-id="56d09-118">您可以建立複本在 hello 相同裝置、 另一個裝置或甚至虛擬機器使用本機或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="56d09-118">You can create a clone on hello same device, another device, or even a virtual machine by using a local or cloud snapshot.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="56d09-119">tooclone 磁碟區</span><span class="sxs-lookup"><span data-stu-id="56d09-119">tooclone a volume</span></span>
1. <span data-ttu-id="56d09-120">在 hello StorSimple Manager 服務頁面上，按一下 hello**備份類別目錄**索引標籤並選取備份組。</span><span class="sxs-lookup"><span data-stu-id="56d09-120">On hello StorSimple Manager service page, click hello **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="56d09-121">展開 hello 備份組 tooview hello 相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-121">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="56d09-122">按一下並選取從 hello 備份集的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-122">Click and select a volume from hello backup set.</span></span>
   
     ![複製磁碟區](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. <span data-ttu-id="56d09-124">按一下**複製**toobegin hello 選取磁碟區複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-124">Click **Clone** toobegin cloning hello selected volume.</span></span>
4. <span data-ttu-id="56d09-125">在 hello 複製磁碟區精靈下**指定名稱和位置**:</span><span class="sxs-lookup"><span data-stu-id="56d09-125">In hello Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="56d09-126">識別目標裝置。</span><span class="sxs-lookup"><span data-stu-id="56d09-126">Identify a target device.</span></span> <span data-ttu-id="56d09-127">這是指將建立 hello 複製 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="56d09-127">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="56d09-128">您可以選擇 hello 相同的裝置，或指定另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="56d09-128">You can choose hello same device or specify another device.</span></span> <span data-ttu-id="56d09-129">如果您選擇其他雲端服務提供者相關聯的磁碟區 (不 Azure) hello 下拉式清單的 hello 目標裝置只會顯示實體裝置。</span><span class="sxs-lookup"><span data-stu-id="56d09-129">If you choose a volume associated with other cloud service providers (not Azure), hello drop-down list for hello target device will only show physical devices.</span></span> <span data-ttu-id="56d09-130">您無法在虛擬裝置上複製與其他雲端服務提供者相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-130">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="56d09-131">請確定所需的 hello 複製 hello 容量低於 hello 目標裝置上可用的 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="56d09-131">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="56d09-132">為複製指定唯一的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="56d09-132">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="56d09-133">hello 名稱必須包含 3 到 127 個字元。</span><span class="sxs-lookup"><span data-stu-id="56d09-133">hello name must contain between 3 and 127 characters.</span></span> 
      
      > [!NOTE]
      > <span data-ttu-id="56d09-134">hello**複製磁碟區做為**欄位就是**分層**即使您正在複製本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-134">hello **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="56d09-135">您無法變更此設定。不過，如果您需要 hello 固定在本機以及複製的磁碟區 toobe，您可以先轉換 hello 複製 tooa 固定在本機磁碟區之後您已成功建立 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-135">You cannot change this setting; however, if you need hello cloned volume toobe locally pinned as well, you can convert hello clone tooa locally pinned volume after you successfully create hello clone.</span></span> <span data-ttu-id="56d09-136">資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="56d09-136">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-manage-volumes-u2.md#change-the-volume-type).</span></span>
      > 
      > 
      
        ![複製精靈 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. <span data-ttu-id="56d09-138">按一下 [hello] 箭號圖示</span><span class="sxs-lookup"><span data-stu-id="56d09-138">Click hello arrow icon</span></span> ![arrow-icon](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) <span data-ttu-id="56d09-140">tooproceed toohello 下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="56d09-140">tooproceed toohello next page.</span></span>
5. <span data-ttu-id="56d09-141">在 [指定可以使用此磁碟區的主機] 下：</span><span class="sxs-lookup"><span data-stu-id="56d09-141">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="56d09-142">指定 hello 複製存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="56d09-142">Specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="56d09-143">您可以新增 ACR，或從 hello 現有清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="56d09-143">You can add a new ACR or choose from hello existing list.</span></span>
      
        ![複製精靈 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. <span data-ttu-id="56d09-145">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="56d09-145">Click hello check icon</span></span> ![核取圖示](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)<span data-ttu-id="56d09-147">toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="56d09-147">toocomplete hello operation.</span></span>
6. <span data-ttu-id="56d09-148">會起始複製工作，且當 hello 複製建立成功時將會通知您。</span><span class="sxs-lookup"><span data-stu-id="56d09-148">A clone job will be initiated and you will be notified when hello clone is successfully created.</span></span> <span data-ttu-id="56d09-149">按一下**檢視工作**toomonitor hello 複製工作上 hello**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="56d09-149">Click **View Job** toomonitor hello clone job on hello **Jobs** page.</span></span> <span data-ttu-id="56d09-150">您會看見 hello hello 複製工作完畢時，下列訊息：</span><span class="sxs-lookup"><span data-stu-id="56d09-150">You will see hello following message when hello clone job is finished:</span></span>
   
    ![複製訊息](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. <span data-ttu-id="56d09-152">複製工作已完成之後 hello:</span><span class="sxs-lookup"><span data-stu-id="56d09-152">After hello clone job is completed:</span></span>
   
   1. <span data-ttu-id="56d09-153">移 toohello**裝置** 頁面上，並選取 hello**磁碟區容器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="56d09-153">Go toohello **Devices** page, and select hello **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="56d09-154">選取 hello 與您用於複製的 hello 來源磁碟區相關聯的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="56d09-154">Select hello volume container that is associated with hello source volume that you cloned.</span></span> <span data-ttu-id="56d09-155">在 hello 清單中的磁碟區，您應該會看到剛才建立的 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-155">In hello list of volumes, you should see hello clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="56d09-156">複製的磁碟區上會自動停用監視和預設備份。</span><span class="sxs-lookup"><span data-stu-id="56d09-156">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="56d09-157">以這種方式建立的複製就是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-157">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="56d09-158">如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。</span><span class="sxs-lookup"><span data-stu-id="56d09-158">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="56d09-159">此複製現在是一般的磁碟區，並可以在磁碟區任何作業都可用於 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-159">This clone is now a regular volume, and any operation that is possible on a volume will be available for hello clone.</span></span> <span data-ttu-id="56d09-160">您需要 tooconfigure 此磁碟區進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="56d09-160">You will need tooconfigure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="56d09-161">暫時性與永久複製</span><span class="sxs-lookup"><span data-stu-id="56d09-161">Transient vs. permanent clones</span></span>
<span data-ttu-id="56d09-162">只有當您正在複製 tooa 不同的裝置時，會建立暫時性的複製品。</span><span class="sxs-lookup"><span data-stu-id="56d09-162">Transient clones are created only when you are cloning tooa different device.</span></span> <span data-ttu-id="56d09-163">您可以複製 hello StorSimple Manager 所管理的備份組的 tooa 不同裝置中的特定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-163">You can clone a specific volume from a backup set tooa different device managed by hello StorSimple Manager.</span></span> <span data-ttu-id="56d09-164">hello 暫時性複本會 hello 原始磁碟區中有參考 toohello 資料和將使用該資料 tooread 並直接在本機寫入 hello 目標裝置上。</span><span class="sxs-lookup"><span data-stu-id="56d09-164">hello transient clone will have references toohello data in hello original volume and will use that data tooread and write locally on hello target device.</span></span> 

<span data-ttu-id="56d09-165">您製作暫時性複本的雲端快照後，將會複製 hello 結果*永久*複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-165">After you take a cloud snapshot of a transient clone, hello resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="56d09-166">在此過程中，一份 hello 資料建立 hello 雲端上 hello 時間 toocopy 這項資料由 hello 資料大小的 hello 和 hello Azure 延遲 （這是 Azure-Azure 複本）。</span><span class="sxs-lookup"><span data-stu-id="56d09-166">During this process, a copy of hello data is created on hello cloud and hello time toocopy this data is determined by hello size of hello data and hello Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="56d09-167">此程序可能需要天 tooweeks。</span><span class="sxs-lookup"><span data-stu-id="56d09-167">This process can take days tooweeks.</span></span> <span data-ttu-id="56d09-168">hello 暫時性複本會變成永久性複本這種方式，而沒有任何參考 toohello 原始磁碟區的資料，從已再製。</span><span class="sxs-lookup"><span data-stu-id="56d09-168">hello transient clone becomes a permanent clone this way and doesn’t have any references toohello original volume data that it was cloned from.</span></span> 

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="56d09-169">暫時性複製與永久複製的案例</span><span class="sxs-lookup"><span data-stu-id="56d09-169">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="56d09-170">hello 下列各節將描述範例可以在其中使用暫時性和永久性複本的情況。</span><span class="sxs-lookup"><span data-stu-id="56d09-170">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="56d09-171">使用暫時性複製復原項目層級</span><span class="sxs-lookup"><span data-stu-id="56d09-171">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="56d09-172">您需要 toorecover 一個年度舊 Microsoft PowerPoint 簡報檔案。</span><span class="sxs-lookup"><span data-stu-id="56d09-172">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="56d09-173">IT 系統管理員識別 hello 從該時間範圍內，特定的備份，然後篩選 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="56d09-173">Your IT administrator identifies hello specific backup from that time frame, and then filters hello volume.</span></span> <span data-ttu-id="56d09-174">hello 系統管理員，然後複製 hello 磁碟區、 找出您要尋找的 hello 檔案並提供它 tooyou。</span><span class="sxs-lookup"><span data-stu-id="56d09-174">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="56d09-175">在此案例中，使用的是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-175">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="56d09-176">![提供的影片](./media/storsimple-clone-volume-u2/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="56d09-176">![Video available](./media/storsimple-clone-volume-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="56d09-177">toowatch 的影片示範如何使用 hello 複製和還原功能在 StorSimple toorecover 刪除檔案中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="56d09-177">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="56d09-178">在 hello 與永久性複本的實際執行環境中測試</span><span class="sxs-lookup"><span data-stu-id="56d09-178">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="56d09-179">您需要 tooverify hello 實際執行環境中測試錯誤。</span><span class="sxs-lookup"><span data-stu-id="56d09-179">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="56d09-180">您建立 hello 實際執行環境中的 hello 磁碟區的複本，然後再採取此複製 toocreate 獨立複製的磁碟區的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="56d09-180">You create a clone of hello volume in hello production environment and then take a cloud snapshot of this clone toocreate an independent cloned volume.</span></span> <span data-ttu-id="56d09-181">在此案例中，使用的是永久複製。</span><span class="sxs-lookup"><span data-stu-id="56d09-181">In this scenario, a permanent clone is used.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="56d09-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56d09-182">Next steps</span></span>
* <span data-ttu-id="56d09-183">了解如何太[StorSimple 磁碟區從備份組還原](storsimple-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="56d09-183">Learn how too[restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="56d09-184">了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="56d09-184">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

