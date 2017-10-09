---
title: "aaaClone StorSimple 8000 系列上的磁碟區 |Microsoft 文件"
description: "描述 hello 複製不同類型和使用方式，並說明如何使用個別的磁碟區的備份組 tooclone StorSimple 8000 系列裝置上。"
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a><span data-ttu-id="132bb-103">在 Azure 入口網站 tooclone 磁碟區中使用 hello StorSimple 裝置管理員服務</span><span class="sxs-lookup"><span data-stu-id="132bb-103">Use hello StorSimple Device Manager service in Azure portal tooclone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="132bb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="132bb-104">Overview</span></span>

<span data-ttu-id="132bb-105">這個教學課程描述如何使用透過 hello 個別磁碟區的備份組 tooclone**備份類別目錄**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="132bb-105">This tutorial describes how you can use a backup set tooclone an individual volume via hello **Backup catalog** blade.</span></span> <span data-ttu-id="132bb-106">它也會說明 hello 差異*暫時性*和*永久*複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-106">It also explains hello difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="132bb-107">本教學課程中的 hello 指導方針適用於 tooall hello StorSimple 8000 系列裝置執行 Update 3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="132bb-107">hello guidance in this tutorial applies tooall hello StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="132bb-108">hello StorSimple 裝置管理員服務**備份類別目錄**刀鋒視窗會顯示所有 hello 的備份組時手動或自動備份所建立的。</span><span class="sxs-lookup"><span data-stu-id="132bb-108">hello StorSimple Device Manager service **Backup catalog** blade displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="132bb-109">然後，您可以在備份組 tooclone 選取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-109">You can then select a volume in a backup set tooclone.</span></span>

 ![備份組清單](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="132bb-111">複製磁碟區的考量</span><span class="sxs-lookup"><span data-stu-id="132bb-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="132bb-112">請考慮 hello 的磁碟區複製時，下列資訊。</span><span class="sxs-lookup"><span data-stu-id="132bb-112">Consider hello following information when cloning a volume.</span></span>

- <span data-ttu-id="132bb-113">複本的行為在 hello 相同與一般磁碟區的方式。</span><span class="sxs-lookup"><span data-stu-id="132bb-113">A clone behaves in hello same way as a regular volume.</span></span> <span data-ttu-id="132bb-114">可以在磁碟區的任何作業是可用於 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-114">Any operation that is possible on a volume is available for hello clone.</span></span>

- <span data-ttu-id="132bb-115">複製的磁碟區上會自動停用監視和預設備份。</span><span class="sxs-lookup"><span data-stu-id="132bb-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="132bb-116">您需要的任何備份 tooconfigure 複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-116">You would need tooconfigure a cloned volume for any backups.</span></span>

- <span data-ttu-id="132bb-117">固定在本機的磁碟區會複製為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="132bb-118">如果您需要 hello 固定在本機複製的磁碟區 toobe，您可以在 hello 複製作業成功完成之後，轉換 hello 複製 tooa 固定在本機磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-118">If you need hello cloned volume toobe locally pinned, you can convert hello clone tooa locally pinned volume after hello clone operation is successfully completed.</span></span> <span data-ttu-id="132bb-119">資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="132bb-119">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="132bb-120">如果您嘗試複製的磁碟區，從階層式 toolocally 釘選之後立即複製 （當它仍然是暫時性複本） 的 tooconvert，hello 轉換會失敗並 hello 下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="132bb-120">If you try tooconvert a cloned volume from tiered toolocally pinned immediately after cloning (when it is still a transient clone), hello conversion fails with hello following error message:</span></span>

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    <span data-ttu-id="132bb-121">只有當您正在複製 tooa 不同裝置上，會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="132bb-121">This error is received only if you are cloning on tooa different device.</span></span> <span data-ttu-id="132bb-122">您可以成功地轉換 hello 磁碟區 toolocally 釘選，如果您先轉換 hello 暫時性複本 tooa 永久性複本。</span><span class="sxs-lookup"><span data-stu-id="132bb-122">You can successfully convert hello volume toolocally pinned if you first convert hello transient clone tooa permanent clone.</span></span> <span data-ttu-id="132bb-123">雲端快照的 hello 暫時性複本 tooconvert 它 tooa 永久性複本。</span><span class="sxs-lookup"><span data-stu-id="132bb-123">Take a cloud snapshot of hello transient clone tooconvert it tooa permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="132bb-124">建立磁碟區複製</span><span class="sxs-lookup"><span data-stu-id="132bb-124">Create a clone of a volume</span></span>

<span data-ttu-id="132bb-125">您可以建立複本在 hello 相同裝置、 另一個裝置或甚至雲端應用裝置，使用本機或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="132bb-125">You can create a clone on hello same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="132bb-126">下列的 hello 程序描述如何 toocreate hello 從複本備份類別目錄。</span><span class="sxs-lookup"><span data-stu-id="132bb-126">hello procedure below describes how toocreate a clone from hello backup catalog.</span></span>  <span data-ttu-id="132bb-127">替代方法 tooinitiate 複製太 toogo**磁碟區**、 選取的磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵並選取**複製**。</span><span class="sxs-lookup"><span data-stu-id="132bb-127">An alternative method tooinitiate clone is toogo too**Volumes**, select a volume, then right-click tooinvoke hello context menu and select **Clone**.</span></span>

<span data-ttu-id="132bb-128">執行 hello hello 備份類別目錄中的下列步驟 toocreate 您的磁碟區的複本。</span><span class="sxs-lookup"><span data-stu-id="132bb-128">Perform hello following steps toocreate a clone of your volume from hello backup catalog.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="132bb-129">tooclone 磁碟區</span><span class="sxs-lookup"><span data-stu-id="132bb-129">tooclone a volume</span></span>

1. <span data-ttu-id="132bb-130">在 tooyour StorSimple 裝置管理員服務的 **備份類別目錄**。</span><span class="sxs-lookup"><span data-stu-id="132bb-130">Go tooyour StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="132bb-131">選取備份組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="132bb-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="132bb-132">選取 hello 適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="132bb-132">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="132bb-133">在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="132bb-133">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="132bb-134">指定 hello 時間範圍。</span><span class="sxs-lookup"><span data-stu-id="132bb-134">Specify hello time range.</span></span>
   4. <span data-ttu-id="132bb-135">按一下**套用**tooexecute 此查詢。</span><span class="sxs-lookup"><span data-stu-id="132bb-135">Click **Apply** tooexecute this query.</span></span>

    <span data-ttu-id="132bb-136">hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。</span><span class="sxs-lookup"><span data-stu-id="132bb-136">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
   
    ![備份組清單](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="132bb-138">展開 hello 備份組 tooview hello 相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-138">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="132bb-139">這些磁碟區必須採取 hello 主機和裝置上離線再進行還原。</span><span class="sxs-lookup"><span data-stu-id="132bb-139">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="132bb-140">存取 hello 磁碟區上 hello**磁碟區**您的裝置，然後遵循 hello 刀鋒視窗中的步驟[使磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)tootake 離線。</span><span class="sxs-lookup"><span data-stu-id="132bb-140">Access hello volumes on hello **Volumes** blade of your device, and then follow hello steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="132bb-141">請確定您已經執行 hello 磁碟區離線 hello 主機上的第一次之後您才能 hello 裝置上的 hello 磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="132bb-141">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="132bb-142">如果您不會在 hello 主機上取得 hello 磁碟區離線，有可能導致 toodata 損毀。</span><span class="sxs-lookup"><span data-stu-id="132bb-142">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   
4. <span data-ttu-id="132bb-143">瀏覽後 toohello**備份類別目錄**和備份組中選取的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-143">Navigate back toohello **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="132bb-144">以滑鼠右鍵按一下，然後從 hello 內容功能表中，選取**複製**。</span><span class="sxs-lookup"><span data-stu-id="132bb-144">Right-click and then from hello context menu, select **Clone**.</span></span>

   ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="132bb-146">在 hello**複製**刀鋒視窗中，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="132bb-146">In hello **Clone** blade, do hello following steps:</span></span>
   
    1. <span data-ttu-id="132bb-147">識別目標裝置。</span><span class="sxs-lookup"><span data-stu-id="132bb-147">Identify a target device.</span></span> <span data-ttu-id="132bb-148">這是指將建立 hello 複製 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="132bb-148">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="132bb-149">您可以選擇 hello 相同的裝置，或指定另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="132bb-149">You can choose hello same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="132bb-150">請確定所需的 hello 複製 hello 容量低於 hello 目標裝置上可用的 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="132bb-150">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
       
    2. <span data-ttu-id="132bb-151">為複製指定唯一的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="132bb-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="132bb-152">hello 名稱必須包含 3 到 127 個字元。</span><span class="sxs-lookup"><span data-stu-id="132bb-152">hello name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="132bb-153">hello**複製磁碟區做為**欄位就是**分層**即使您正在複製本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-153">hello **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="132bb-154">您無法變更此設定。不過，如果您需要 hello 固定在本機以及複製的磁碟區 toobe，您可以先轉換 hello 複製 tooa 固定在本機磁碟區之後您已成功建立 hello 複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-154">You cannot change this setting; however, if you need hello cloned volume toobe locally pinned as well, you can convert hello clone tooa locally pinned volume after you successfully create hello clone.</span></span> <span data-ttu-id="132bb-155">資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="132bb-155">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="132bb-156">在下**連線主機**，指定 hello 複製存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="132bb-156">Under **Connected hosts**, specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="132bb-157">您可以新增 ACR，或從 hello 現有清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="132bb-157">You can add a new ACR or choose from hello existing list.</span></span> <span data-ttu-id="132bb-158">hello ACR 會決定可存取此複本的主機。</span><span class="sxs-lookup"><span data-stu-id="132bb-158">hello ACR will determine which hosts can access this clone.</span></span>
      
        ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="132bb-160">按一下**複製**toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="132bb-160">Click **Clone** toocomplete hello operation.</span></span>

4. <span data-ttu-id="132bb-161">複製工作已起始，而且當 hello 複製建立成功時，會收到通知。</span><span class="sxs-lookup"><span data-stu-id="132bb-161">A clone job is initiated and you are notified when hello clone is successfully created.</span></span> <span data-ttu-id="132bb-162">按一下 hello 工作通知或太到**作業**刀鋒視窗 toomonitor hello 複製工作。</span><span class="sxs-lookup"><span data-stu-id="132bb-162">Click hello job notification or go too**Jobs** blade toomonitor hello clone job.</span></span>

    ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="132bb-164">Hello 複製工作完畢之後，移 tooyour 裝置，然後按一下**磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="132bb-164">After hello clone job is complete, go tooyour device and then click **Volumes**.</span></span> <span data-ttu-id="132bb-165">在 [hello] 清單中的磁碟區，您應該會看到剛建立 hello 中相同的 hello 複製 hello 來源磁碟區的磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="132bb-165">In hello list of volumes, you should see hello clone that was just created in hello same volume container that has hello source volume.</span></span>

    ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="132bb-167">以這種方式建立的複製就是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="132bb-168">如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。</span><span class="sxs-lookup"><span data-stu-id="132bb-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="132bb-169">暫時性與永久複製</span><span class="sxs-lookup"><span data-stu-id="132bb-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="132bb-170">只有當您複製 tooanother 裝置時，會建立暫時性的複製品。</span><span class="sxs-lookup"><span data-stu-id="132bb-170">Transient clones are created only when you clone tooanother device.</span></span> <span data-ttu-id="132bb-171">您可以複製 hello StorSimple 裝置管理員所管理的備份組的 tooa 不同裝置中的特定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-171">You can clone a specific volume from a backup set tooa different device managed by hello StorSimple Device Manager.</span></span> <span data-ttu-id="132bb-172">hello 暫時性複本 hello 原始磁碟區中有參考 toohello 資料，並使用該資料 tooread 和寫入本機 hello 目標裝置上。</span><span class="sxs-lookup"><span data-stu-id="132bb-172">hello transient clone has references toohello data in hello original volume and uses that data tooread and write locally on hello target device.</span></span>

<span data-ttu-id="132bb-173">您製作暫時性複本的雲端快照後，複製 hello 結果是*永久*複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-173">After you take a cloud snapshot of a transient clone, hello resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="132bb-174">在此過程中，一份 hello 資料建立 hello 雲端上 hello 時間 toocopy 這項資料由 hello 資料大小的 hello 和 hello Azure 延遲 （這是 Azure-Azure 複本）。</span><span class="sxs-lookup"><span data-stu-id="132bb-174">During this process, a copy of hello data is created on hello cloud and hello time toocopy this data is determined by hello size of hello data and hello Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="132bb-175">此程序可能需要天 tooweeks。</span><span class="sxs-lookup"><span data-stu-id="132bb-175">This process can take days tooweeks.</span></span> <span data-ttu-id="132bb-176">hello 暫時性複本會變成永久性複本，而沒有任何參考 toohello 原始磁碟區的資料，從已再製。</span><span class="sxs-lookup"><span data-stu-id="132bb-176">hello transient clone becomes a permanent clone and doesn’t have any references toohello original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="132bb-177">暫時性複製與永久複製的案例</span><span class="sxs-lookup"><span data-stu-id="132bb-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="132bb-178">hello 下列各節將描述範例可以在其中使用暫時性和永久性複本的情況。</span><span class="sxs-lookup"><span data-stu-id="132bb-178">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="132bb-179">使用暫時性複製復原項目層級</span><span class="sxs-lookup"><span data-stu-id="132bb-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="132bb-180">您需要 toorecover 一個年度舊 Microsoft PowerPoint 簡報檔案。</span><span class="sxs-lookup"><span data-stu-id="132bb-180">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="132bb-181">IT 系統管理員識別 hello 這段時間，從特定的備份，然後篩選 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="132bb-181">Your IT administrator identifies hello specific backup from that time, and then filters hello volume.</span></span> <span data-ttu-id="132bb-182">hello 系統管理員，然後複製 hello 磁碟區、 找出您要尋找的 hello 檔案並提供它 tooyou。</span><span class="sxs-lookup"><span data-stu-id="132bb-182">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="132bb-183">在此案例中，使用的是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="132bb-184">在 hello 與永久性複本的實際執行環境中測試</span><span class="sxs-lookup"><span data-stu-id="132bb-184">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="132bb-185">您需要 tooverify hello 實際執行環境中測試錯誤。</span><span class="sxs-lookup"><span data-stu-id="132bb-185">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="132bb-186">您建立 hello 實際執行環境中的 hello 磁碟區的複本，然後再採取此複製 toocreate 獨立複製的磁碟區的雲端快照。</span><span class="sxs-lookup"><span data-stu-id="132bb-186">You create a clone of hello volume in hello production environment and then take a cloud snapshot of this clone toocreate an independent cloned volume.</span></span> <span data-ttu-id="132bb-187">在此案例中，使用的是永久複製。</span><span class="sxs-lookup"><span data-stu-id="132bb-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="132bb-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="132bb-188">Next steps</span></span>
* <span data-ttu-id="132bb-189">了解如何太[StorSimple 磁碟區從備份組還原](storsimple-8000-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="132bb-189">Learn how too[restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="132bb-190">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="132bb-190">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

