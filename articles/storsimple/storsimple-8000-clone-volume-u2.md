---
title: "複製 StorSimple 8000 系列的磁碟區 | Microsoft Docs"
description: "說明不同的複製類型以及使用方式，並說明如何使用備份組來複製 StorSimple 8000 系列裝置上的個別磁碟區。"
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
ms.openlocfilehash: 70c85bcb2c26d2ad3d0515d24e028f84495634c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-clone-a-volume"></a><span data-ttu-id="28f2f-103">在 Azure 入口網站中，使用 StorSimple 裝置管理員服務來複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="28f2f-103">Use the StorSimple Device Manager service in Azure portal to clone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="28f2f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="28f2f-104">Overview</span></span>

<span data-ttu-id="28f2f-105">本教學課程說明如何透過 [備份類別目錄] 刀鋒視窗使用備份組來複製個別磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-105">This tutorial describes how you can use a backup set to clone an individual volume via the **Backup catalog** blade.</span></span> <span data-ttu-id="28f2f-106">它也會說明「暫時性」與「永久」複製之間的差異。</span><span class="sxs-lookup"><span data-stu-id="28f2f-106">It also explains the difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="28f2f-107">本教學課程中的指導適用於執行 Update 3 或更新版本的所有 StorSimple 8000 系列裝置。</span><span class="sxs-lookup"><span data-stu-id="28f2f-107">The guidance in this tutorial applies to all the StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="28f2f-108">StorSimple 裝置管理員服務 [備份類別目錄]  刀鋒視窗會顯示在進行手動或自動備份時所建立的所有備份組。</span><span class="sxs-lookup"><span data-stu-id="28f2f-108">The StorSimple Device Manager service **Backup catalog** blade displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="28f2f-109">然後您可以在備份組中選取要複製的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-109">You can then select a volume in a backup set to clone.</span></span>

 ![備份組清單](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="28f2f-111">複製磁碟區的考量</span><span class="sxs-lookup"><span data-stu-id="28f2f-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="28f2f-112">複製磁碟區之前，請考量下列資訊。</span><span class="sxs-lookup"><span data-stu-id="28f2f-112">Consider the following information when cloning a volume.</span></span>

- <span data-ttu-id="28f2f-113">複製的磁碟區行為方式與一般磁碟區相同。</span><span class="sxs-lookup"><span data-stu-id="28f2f-113">A clone behaves in the same way as a regular volume.</span></span> <span data-ttu-id="28f2f-114">在磁碟區上可進行的任何作業皆可用於複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-114">Any operation that is possible on a volume is available for the clone.</span></span>

- <span data-ttu-id="28f2f-115">複製的磁碟區上會自動停用監視和預設備份。</span><span class="sxs-lookup"><span data-stu-id="28f2f-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="28f2f-116">進行任何備份時您都必須設定複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-116">You would need to configure a cloned volume for any backups.</span></span>

- <span data-ttu-id="28f2f-117">固定在本機的磁碟區會複製為分層磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="28f2f-118">如果您需要將複製的磁碟區固定在本機，可以在複製作業成功完成之後，再將複製品轉換為固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-118">If you need the cloned volume to be locally pinned, you can convert the clone to a locally pinned volume after the clone operation is successfully completed.</span></span> <span data-ttu-id="28f2f-119">如需將分層磁碟區轉換為固定在本機的磁碟區的詳細資訊，請移至 [變更磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-119">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="28f2f-120">如果您嘗試在複製之後 (當其仍為暫時性複製) 立即將分層磁碟區轉換為固定在本機的磁碟區，則轉換會失敗並出現下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="28f2f-120">If you try to convert a cloned volume from tiered to locally pinned immediately after cloning (when it is still a transient clone), the conversion fails with the following error message:</span></span>

    `Unable to modify the usage type for volume {0}. This can happen if the volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry the modify operation.`

    <span data-ttu-id="28f2f-121">只有在您複製到不同裝置時才會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="28f2f-121">This error is received only if you are cloning on to a different device.</span></span> <span data-ttu-id="28f2f-122">先將暫時性複製品轉換為永久複製品，即可成功將磁碟區轉換為固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-122">You can successfully convert the volume to locally pinned if you first convert the transient clone to a permanent clone.</span></span> <span data-ttu-id="28f2f-123">請拍下暫時性複製的雲端快照，以將其轉換為永久複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-123">Take a cloud snapshot of the transient clone to convert it to a permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="28f2f-124">建立磁碟區複製</span><span class="sxs-lookup"><span data-stu-id="28f2f-124">Create a clone of a volume</span></span>

<span data-ttu-id="28f2f-125">您可以使用本機或雲端快照，在相同的裝置、另一個裝置，甚或雲端設備上建立複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-125">You can create a clone on the same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="28f2f-126">下列程序描述如何從備份類別目錄建立複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-126">The procedure below describes how to create a clone from the backup catalog.</span></span>  <span data-ttu-id="28f2f-127">起始複製的替代方法是移至 [磁碟區]，選取磁碟區，然後按一下滑鼠右鍵以叫用操作功能表，然後選取 [複製]。</span><span class="sxs-lookup"><span data-stu-id="28f2f-127">An alternative method to initiate clone is to go to **Volumes**, select a volume, then right-click to invoke the context menu and select **Clone**.</span></span>

<span data-ttu-id="28f2f-128">執行下列步驟，以從備份類別目錄中建立您的磁碟區的複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-128">Perform the following steps to create a clone of your volume from the backup catalog.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="28f2f-129">若要複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="28f2f-129">To clone a volume</span></span>

1. <span data-ttu-id="28f2f-130">移至 StorSimple 裝置管理員服務，然後按一下 [備份類別目錄]。</span><span class="sxs-lookup"><span data-stu-id="28f2f-130">Go to your StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="28f2f-131">選取備份組，如下所示：</span><span class="sxs-lookup"><span data-stu-id="28f2f-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="28f2f-132">選取適當的裝置。</span><span class="sxs-lookup"><span data-stu-id="28f2f-132">Select the appropriate device.</span></span>
   2. <span data-ttu-id="28f2f-133">在下拉式清單中，針對要選取的備份選擇磁碟區或備份原則。</span><span class="sxs-lookup"><span data-stu-id="28f2f-133">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="28f2f-134">指定時間範圍。</span><span class="sxs-lookup"><span data-stu-id="28f2f-134">Specify the time range.</span></span>
   4. <span data-ttu-id="28f2f-135">按一下 [套用] 以執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="28f2f-135">Click **Apply** to execute this query.</span></span>

    <span data-ttu-id="28f2f-136">與選取的磁碟區或備份原則相關聯的備份應該會出現在備份組清單中。</span><span class="sxs-lookup"><span data-stu-id="28f2f-136">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
   
    ![備份組清單](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="28f2f-138">展開備份組以檢視相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-138">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="28f2f-139">您必須先在主機和裝置上將這些磁碟區離線，才能還原它們。</span><span class="sxs-lookup"><span data-stu-id="28f2f-139">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="28f2f-140">存取您裝置上 [磁碟區] 刀鋒視窗上的磁碟區，然後依照[讓磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)中的步驟來讓它們離線。</span><span class="sxs-lookup"><span data-stu-id="28f2f-140">Access the volumes on the **Volumes** blade of your device, and then follow the steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) to take them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="28f2f-141">確定您已先讓主機上的磁碟區離線，然後再讓裝置上的磁碟區離線。</span><span class="sxs-lookup"><span data-stu-id="28f2f-141">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="28f2f-142">如果您並未讓主機上的磁碟區離線，可能會導致資料損毀。</span><span class="sxs-lookup"><span data-stu-id="28f2f-142">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   
4. <span data-ttu-id="28f2f-143">瀏覽回到 [備份類別目錄]，並選取備份組中的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-143">Navigate back to the **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="28f2f-144">以滑鼠右鍵按一下，然後從操作功能表中選取 [複製]。</span><span class="sxs-lookup"><span data-stu-id="28f2f-144">Right-click and then from the context menu, select **Clone**.</span></span>

   ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="28f2f-146">在 [複製] 刀鋒視窗中，執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="28f2f-146">In the **Clone** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="28f2f-147">識別目標裝置。</span><span class="sxs-lookup"><span data-stu-id="28f2f-147">Identify a target device.</span></span> <span data-ttu-id="28f2f-148">這是即將建立複製的位置。</span><span class="sxs-lookup"><span data-stu-id="28f2f-148">This is the location where the clone will be created.</span></span> <span data-ttu-id="28f2f-149">您可以選擇相同的裝置，或指定另一個裝置。</span><span class="sxs-lookup"><span data-stu-id="28f2f-149">You can choose the same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="28f2f-150">確定要複製的容量小於目標裝置中可用的容量。</span><span class="sxs-lookup"><span data-stu-id="28f2f-150">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
       
    2. <span data-ttu-id="28f2f-151">為複製指定唯一的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="28f2f-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="28f2f-152">此名稱必須包含 3 到 127 個字元。</span><span class="sxs-lookup"><span data-stu-id="28f2f-152">The name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="28f2f-153">即使您複製了本機釘選磁碟區，[將磁碟區複製為] 欄位仍然會**分層**。</span><span class="sxs-lookup"><span data-stu-id="28f2f-153">The **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="28f2f-154">您無法變更此設定，但如果您需要在本機釘選複製的磁碟區，您可以在成功建立複製之後，將複製轉換到本機釘選的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-154">You cannot change this setting; however, if you need the cloned volume to be locally pinned as well, you can convert the clone to a locally pinned volume after you successfully create the clone.</span></span> <span data-ttu-id="28f2f-155">如需將分層磁碟區轉換為固定在本機的磁碟區的詳細資訊，請移至 [變更磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-155">For information about converting a tiered volume to a locally pinned volume, go to [Change the volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="28f2f-156">在 [已連線的主機] 下，指定該複製的存取控制記錄 (ACR)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-156">Under **Connected hosts**, specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="28f2f-157">您可以加入新的 ACR，或從現有清單中選擇。</span><span class="sxs-lookup"><span data-stu-id="28f2f-157">You can add a new ACR or choose from the existing list.</span></span> <span data-ttu-id="28f2f-158">ACR 會決定可存取此複製的主機。</span><span class="sxs-lookup"><span data-stu-id="28f2f-158">The ACR will determine which hosts can access this clone.</span></span>
      
        ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="28f2f-160">按一下 [複製]，以完成作業。</span><span class="sxs-lookup"><span data-stu-id="28f2f-160">Click **Clone** to complete the operation.</span></span>

4. <span data-ttu-id="28f2f-161">複製作業隨即起始，並在成功建立複製時通知您。</span><span class="sxs-lookup"><span data-stu-id="28f2f-161">A clone job is initiated and you are notified when the clone is successfully created.</span></span> <span data-ttu-id="28f2f-162">按一下作業通知，或移至 [作業] 刀鋒視窗以監控複製作業。</span><span class="sxs-lookup"><span data-stu-id="28f2f-162">Click the job notification or go to **Jobs** blade to monitor the clone job.</span></span>

    ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="28f2f-164">複製作業完成後，移至您的裝置，然後按一下 [磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="28f2f-164">After the clone job is complete, go to your device and then click **Volumes**.</span></span> <span data-ttu-id="28f2f-165">在磁碟區清單中，您應該會看見剛剛在相同磁碟區容器中建立的複製具有來源磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-165">In the list of volumes, you should see the clone that was just created in the same volume container that has the source volume.</span></span>

    ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="28f2f-167">以這種方式建立的複製就是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="28f2f-168">如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="28f2f-169">暫時性與永久複製</span><span class="sxs-lookup"><span data-stu-id="28f2f-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="28f2f-170">只有在您複製到另一個裝置時，才會建立暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-170">Transient clones are created only when you clone to another device.</span></span> <span data-ttu-id="28f2f-171">您可以從備份組複製特定磁碟區到受 StorSimple 裝置管理員管理的不同裝置。</span><span class="sxs-lookup"><span data-stu-id="28f2f-171">You can clone a specific volume from a backup set to a different device managed by the StorSimple Device Manager.</span></span> <span data-ttu-id="28f2f-172">暫時性複製有原始磁碟區中資料的參考，並使用該資料在本機的目標裝置上讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="28f2f-172">The transient clone has references to the data in the original volume and uses that data to read and write locally on the target device.</span></span>

<span data-ttu-id="28f2f-173">在建立暫時性複製的雲端快照之後，產生的複製就是「永久」 複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-173">After you take a cloud snapshot of a transient clone, the resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="28f2f-174">在此程序中，會在雲端建立資料複本，而複製此資料的時機則由資料大小和 Azure 的延遲來決定 (這是 Azure 對 Azure 複製)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-174">During this process, a copy of the data is created on the cloud and the time to copy this data is determined by the size of the data and the Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="28f2f-175">此程序可能需要數天至數週。</span><span class="sxs-lookup"><span data-stu-id="28f2f-175">This process can take days to weeks.</span></span> <span data-ttu-id="28f2f-176">暫時性複製會成為永久複製，且沒有對所複製原始磁碟區資料的任何參考。</span><span class="sxs-lookup"><span data-stu-id="28f2f-176">The transient clone becomes a permanent clone and doesn’t have any references to the original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="28f2f-177">暫時性複製與永久複製的案例</span><span class="sxs-lookup"><span data-stu-id="28f2f-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="28f2f-178">下列各節將說明可使用暫時性複製與永久複製的範例情況。</span><span class="sxs-lookup"><span data-stu-id="28f2f-178">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="28f2f-179">使用暫時性複製復原項目層級</span><span class="sxs-lookup"><span data-stu-id="28f2f-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="28f2f-180">您要復原過去一年的 Microsoft PowerPoint 簡報檔案。</span><span class="sxs-lookup"><span data-stu-id="28f2f-180">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="28f2f-181">IT 系統管理員會辨識該時間內的特定備份，然後篩選磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-181">Your IT administrator identifies the specific backup from that time, and then filters the volume.</span></span> <span data-ttu-id="28f2f-182">系統管理員接著再複製磁碟區，找出您要找的檔案再提供給您。</span><span class="sxs-lookup"><span data-stu-id="28f2f-182">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="28f2f-183">在此案例中，使用的是暫時性複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="28f2f-184">利用永久複製在實際執行環境中進行測試</span><span class="sxs-lookup"><span data-stu-id="28f2f-184">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="28f2f-185">您需要確認生產環境中的測試錯誤。</span><span class="sxs-lookup"><span data-stu-id="28f2f-185">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="28f2f-186">您在生產環境中建立磁碟區的複製，並採用這個複製的雲端快照來建立獨立的複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="28f2f-186">You create a clone of the volume in the production environment and then take a cloud snapshot of this clone to create an independent cloned volume.</span></span> <span data-ttu-id="28f2f-187">在此案例中，使用的是永久複製。</span><span class="sxs-lookup"><span data-stu-id="28f2f-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28f2f-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28f2f-188">Next steps</span></span>
* <span data-ttu-id="28f2f-189">了解如何 [從備份組還原 StorSimple 磁碟區](storsimple-8000-restore-from-backup-set-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-189">Learn how to [restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="28f2f-190">了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="28f2f-190">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

