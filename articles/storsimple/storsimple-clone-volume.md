---
title: "aaaClone 您的 StorSimple 磁碟區 |Microsoft 文件"
description: "描述 hello 複製不同類型和當 toouse 它們，並說明如何使用備份組 tooclone 個別磁碟區。"
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
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a><span data-ttu-id="e9466-103">使用 hello StorSimple Manager 服務 tooclone 磁碟區</span><span class="sxs-lookup"><span data-stu-id="e9466-103">Use hello StorSimple Manager service tooclone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="e9466-104">概觀</span><span class="sxs-lookup"><span data-stu-id="e9466-104">Overview</span></span>
<span data-ttu-id="e9466-105">StorSimple Manager 服務的 hello**備份類別目錄**頁面會顯示所有 hello 的備份組時手動或自動備份所建立的。</span><span class="sxs-lookup"><span data-stu-id="e9466-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="e9466-106">您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e9466-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

![備份類別目錄頁面](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="e9466-108">本教學課程說明如何使用備份組 tooclone 個別磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e9466-108">This tutorial describes how you can use a backup set tooclone an individual volume.</span></span> <span data-ttu-id="e9466-109">它也會說明 hello 差異*暫時性*和*永久*複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-109">It also explains hello difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="e9466-110">建立磁碟區複製</span><span class="sxs-lookup"><span data-stu-id="e9466-110">Create a clone of a volume</span></span>
<span data-ttu-id="e9466-111">您可以建立複本上 hello 相同裝置、 另一個裝置或甚至虛擬機器使用本機或雲端快照。</span><span class="sxs-lookup"><span data-stu-id="e9466-111">You can create a clone on hello same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="e9466-112">tooclone 磁碟區</span><span class="sxs-lookup"><span data-stu-id="e9466-112">tooclone a volume</span></span>
1. <span data-ttu-id="e9466-113">在 hello StorSimple Manager 服務頁面上，按一下 hello**備份類別目錄**索引標籤並選取備份組。</span><span class="sxs-lookup"><span data-stu-id="e9466-113">On hello StorSimple Manager service page, click hello **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="e9466-114">展開 hello 備份組 tooview hello 相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e9466-114">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="e9466-115">按一下並選取從 hello 備份集的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e9466-115">Click and select a volume from hello backup set.</span></span>
   
     ![複製磁碟區](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="e9466-117">按一下**複製**toobegin hello 選取磁碟區複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-117">Click **Clone** toobegin cloning hello selected volume.</span></span>
4. <span data-ttu-id="e9466-118">在 hello 複製磁碟區精靈下**指定名稱和位置**:</span><span class="sxs-lookup"><span data-stu-id="e9466-118">In hello Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="e9466-119">識別目標裝置。</span><span class="sxs-lookup"><span data-stu-id="e9466-119">Identify a target device.</span></span> <span data-ttu-id="e9466-120">這是指將建立 hello 複製 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="e9466-120">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="e9466-121">您可以選擇 hello 相同的裝置，或指定另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="e9466-121">You can choose hello same device or specify another device.</span></span> <span data-ttu-id="e9466-122">如果您選擇其他雲端服務提供者相關聯的磁碟區 (不 Azure) hello 下拉式清單的 hello 目標裝置只會顯示實體裝置。</span><span class="sxs-lookup"><span data-stu-id="e9466-122">If you choose a volume associated with other cloud service providers (not Azure), hello drop-down list for hello target device will only show physical devices.</span></span> <span data-ttu-id="e9466-123">您無法在虛擬裝置上複製與其他雲端服務提供者相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e9466-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e9466-124">請確定所需的 hello 複製 hello 容量低於 hello 目標裝置上可用的 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="e9466-124">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="e9466-125">為複製指定唯一的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="e9466-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="e9466-126">hello 名稱必須包含 3 到 127 個字元。</span><span class="sxs-lookup"><span data-stu-id="e9466-126">hello name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="e9466-127">按一下 [hello] 箭號圖示</span><span class="sxs-lookup"><span data-stu-id="e9466-127">Click hello arrow icon</span></span> ![arrow-icon](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="e9466-129">tooproceed toohello 下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="e9466-129">tooproceed toohello next page.</span></span>
5. <span data-ttu-id="e9466-130">在 [指定可以使用此磁碟區的主機] 下：</span><span class="sxs-lookup"><span data-stu-id="e9466-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="e9466-131">指定 hello 複製存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="e9466-131">Specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="e9466-132">您可以新增 ACR，或從 hello 現有清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="e9466-132">You can add a new ACR or choose from hello existing list.</span></span>
   2. <span data-ttu-id="e9466-133">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="e9466-133">Click hello check icon</span></span> ![核取圖示](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="e9466-135">toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e9466-135">toocomplete hello operation.</span></span>
6. <span data-ttu-id="e9466-136">會起始複製工作，且當 hello 複製建立成功時將會通知您。</span><span class="sxs-lookup"><span data-stu-id="e9466-136">A clone job will be initiated and you will be notified when hello clone is successfully created.</span></span> <span data-ttu-id="e9466-137">按一下**檢視工作**toomonitor hello 複製工作上 hello**作業**頁面。</span><span class="sxs-lookup"><span data-stu-id="e9466-137">Click **View Job** toomonitor hello clone job on hello **Jobs** page.</span></span>
7. <span data-ttu-id="e9466-138">複製工作已完成之後 hello:</span><span class="sxs-lookup"><span data-stu-id="e9466-138">After hello clone job is completed:</span></span>
   
   1. <span data-ttu-id="e9466-139">移 toohello**裝置** 頁面上，並選取 hello**磁碟區容器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e9466-139">Go toohello **Devices** page, and select hello **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="e9466-140">選取 hello 與您用於複製的 hello 來源磁碟區相關聯的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="e9466-140">Select hello volume container that is associated with hello source volume that you cloned.</span></span> <span data-ttu-id="e9466-141">在 hello 清單中的磁碟區，您應該會看到剛才建立的 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-141">In hello list of volumes, you should see hello clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="e9466-142">複製的磁碟區上會自動停用監視和預設備份。</span><span class="sxs-lookup"><span data-stu-id="e9466-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="e9466-143">以這種方式建立的複製就是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="e9466-144">如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。</span><span class="sxs-lookup"><span data-stu-id="e9466-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="e9466-145">此複製現在是一般的磁碟區，並可以在磁碟區任何作業都可用於 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for hello clone.</span></span> <span data-ttu-id="e9466-146">您需要 tooconfigure 此磁碟區進行任何備份。</span><span class="sxs-lookup"><span data-stu-id="e9466-146">You will need tooconfigure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="e9466-147">暫時性與永久複製</span><span class="sxs-lookup"><span data-stu-id="e9466-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="e9466-148">只有當您正在複製 tooa 不同裝置上時，會建立暫時性和永久性複本。</span><span class="sxs-lookup"><span data-stu-id="e9466-148">Transient and permanent clones are created only when you are cloning on tooa different device.</span></span> <span data-ttu-id="e9466-149">您可以複製特定的磁碟區從備份組 tooa 不同的裝置。</span><span class="sxs-lookup"><span data-stu-id="e9466-149">You can clone a specific volume from a backup set tooa different device.</span></span> <span data-ttu-id="e9466-150">以這種方式建立的複製就是「暫時性」  複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="e9466-151">hello 暫時性複本會有參考 toohello 原始磁碟區，並使用該磁碟區 tooread 在本機寫入。</span><span class="sxs-lookup"><span data-stu-id="e9466-151">hello transient clone will have references toohello original volume and will use that volume tooread while writing locally.</span></span> 

<span data-ttu-id="e9466-152">您製作暫時性複本的雲端快照後，將會複製 hello 結果*永久*複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-152">After you take a cloud snapshot of a transient clone, hello resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="e9466-153">hello 永久性複本是獨立的且沒有任何參考 toohello 原始磁碟區複製從。</span><span class="sxs-lookup"><span data-stu-id="e9466-153">hello permanent clone is independent and doesn’t have any references toohello original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="e9466-154">暫時性複製與永久複製的案例</span><span class="sxs-lookup"><span data-stu-id="e9466-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="e9466-155">hello 下列各節將描述範例可以在其中使用暫時性和永久性複本的情況。</span><span class="sxs-lookup"><span data-stu-id="e9466-155">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="e9466-156">使用暫時性複製復原項目層級</span><span class="sxs-lookup"><span data-stu-id="e9466-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="e9466-157">您需要 toorecover 一個年度舊 Microsoft PowerPoint 簡報檔案。</span><span class="sxs-lookup"><span data-stu-id="e9466-157">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="e9466-158">IT 系統管理員識別 hello 從該時間範圍內，特定的備份，然後篩選 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e9466-158">Your IT administrator identifies hello specific backup from that time frame, and then filters hello volume.</span></span> <span data-ttu-id="e9466-159">hello 系統管理員，然後複製 hello 磁碟區、 找出您要尋找的 hello 檔案並提供它 tooyou。</span><span class="sxs-lookup"><span data-stu-id="e9466-159">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="e9466-160">在此案例中，使用的是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="e9466-161">![提供的影片](./media/storsimple-clone-volume/Video_icon.png) **提供的影片**</span><span class="sxs-lookup"><span data-stu-id="e9466-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="e9466-162">toowatch 的影片示範如何使用 hello 複製和還原功能在 StorSimple toorecover 刪除檔案中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="e9466-162">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="e9466-163">在 hello 與永久性複本的實際執行環境中測試</span><span class="sxs-lookup"><span data-stu-id="e9466-163">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="e9466-164">您需要 tooverify hello 實際執行環境中測試錯誤。</span><span class="sxs-lookup"><span data-stu-id="e9466-164">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="e9466-165">您建立 hello 磁碟區的複本，您可以在 hello 生產環境中此複本的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="e9466-165">You create a clone of hello volume in hello production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="e9466-166">hello 複製的磁碟區現在已獨立。</span><span class="sxs-lookup"><span data-stu-id="e9466-166">hello cloned volume is now independent.</span></span> <span data-ttu-id="e9466-167">在此案例中，使用的是永久複製。</span><span class="sxs-lookup"><span data-stu-id="e9466-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9466-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9466-168">Next steps</span></span>
* <span data-ttu-id="e9466-169">了解如何太[StorSimple 磁碟區從備份組還原](storsimple-restore-from-backup-set.md)。</span><span class="sxs-lookup"><span data-stu-id="e9466-169">Learn how too[restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="e9466-170">了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="e9466-170">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

