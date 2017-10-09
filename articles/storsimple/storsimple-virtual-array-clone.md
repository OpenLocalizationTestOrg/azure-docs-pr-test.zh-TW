---
title: "aaaClone StorSimple Virtual Array 備份 |Microsoft 文件"
description: "深入了解如何 tooclone 備份和復原的檔案從您的 StorSimple Virtual Array。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a><span data-ttu-id="5ce5b-103">從 StorSimple Virtual Array 的備份複製</span><span class="sxs-lookup"><span data-stu-id="5ce5b-103">Clone from a backup of your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="5ce5b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5ce5b-104">Overview</span></span>

<span data-ttu-id="5ce5b-105">本文逐步如何 tooclone 備份您的共用或磁碟區上設定您 Microsoft Azure StorSimple Virtual Array。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-105">This article describes step-by-step how tooclone a backup set of your shares or volumes on your Microsoft Azure StorSimple Virtual Array.</span></span> <span data-ttu-id="5ce5b-106">hello 複製的備份是使用的 toorecover 已刪除或遺失的檔案。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-106">hello cloned backup is used toorecover a deleted or lost file.</span></span> <span data-ttu-id="5ce5b-107">hello 發行項也會包含詳細的步驟 tooperform StorSimple 虛擬陣列上的項目層級復原設定為檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-107">hello article also includes detailed steps tooperform an item-level recovery on your StorSimple Virtual Array configured as a file server.</span></span>

## <a name="clone-shares-from-a-backup-set"></a><span data-ttu-id="5ce5b-108">從備份組複製共用</span><span class="sxs-lookup"><span data-stu-id="5ce5b-108">Clone shares from a backup set</span></span>

<span data-ttu-id="5ce5b-109">**您嘗試 tooclone 共用之前，請確定您有足夠的空間 hello 裝置 toocomplete 這項作業。**</span><span class="sxs-lookup"><span data-stu-id="5ce5b-109">**Before you try tooclone shares, ensure that you have sufficient space on hello device toocomplete this operation.**</span></span> <span data-ttu-id="5ce5b-110">從備份中 hello tooclone [Azure 入口網站](https://portal.azure.com/)，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-110">tooclone from a backup, in hello [Azure portal](https://portal.azure.com/), perform hello following steps.</span></span>

#### <a name="tooclone-a-share"></a><span data-ttu-id="5ce5b-111">tooclone 共用</span><span class="sxs-lookup"><span data-stu-id="5ce5b-111">tooclone a share</span></span>

1. <span data-ttu-id="5ce5b-112">瀏覽過**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-112">Browse too**Devices** blade.</span></span> <span data-ttu-id="5ce5b-113">選取並按一下您的裝置，然後按一下共用。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-113">Select and click your device and then click **Shares**.</span></span> <span data-ttu-id="5ce5b-114">選取您想 tooclone，以滑鼠右鍵按一下 hello 共用 tooinvoke hello 內容功能表的 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-114">Select hello share that you want tooclone, right-click hello share tooinvoke hello context menu.</span></span> <span data-ttu-id="5ce5b-115">選取 [複製]。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-115">Select **Clone**.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. <span data-ttu-id="5ce5b-117">在 hello**複製**刀鋒視窗中，按一下**備份 > 選取**和執行然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5ce5b-117">In hello **Clone** blade, click **Backup > Select** and then do hello following:</span></span> 
   
   <span data-ttu-id="5ce5b-118">a.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-118">a.</span></span>    <span data-ttu-id="5ce5b-119">篩選這個 hello 時間範圍為基礎的裝置上的備份。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-119">Filter a backup on this device based on hello time range.</span></span> <span data-ttu-id="5ce5b-120">您可以選擇 [過去 7 天]、[過去 30 天] 和 [過去一年]。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-120">You can choose from **Past 7 days**, **Past 30 days**, and **Past year**.</span></span>
   
   <span data-ttu-id="5ce5b-121">b.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-121">b.</span></span>    <span data-ttu-id="5ce5b-122">Hello 在清單中顯示篩選過的備份，選取 從備份 tooclone。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-122">In hello list of filtered backups displayed, select a backup tooclone from.</span></span>
   
   <span data-ttu-id="5ce5b-123">c.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-123">c.</span></span>    <span data-ttu-id="5ce5b-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-124">Click **OK**.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. <span data-ttu-id="5ce5b-126">在 hello**複製**刀鋒視窗中，按一下 **目標設定**和執行然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5ce5b-126">In hello **Clone** blade, click **Target settings** and then do hello following:</span></span>
   
   <span data-ttu-id="5ce5b-127">a.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-127">a.</span></span>    <span data-ttu-id="5ce5b-128">提供共用名稱。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-128">Provide a share name.</span></span> <span data-ttu-id="5ce5b-129">hello 共用名稱必須包含 3-127 個字元。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-129">hello share name must contain 3-127 characters.</span></span>
   
   <span data-ttu-id="5ce5b-130">b.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-130">b.</span></span>    <span data-ttu-id="5ce5b-131">選擇性地提供 hello 複製共用的描述。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-131">Optionally provide a description for hello cloned share.</span></span>
   
   <span data-ttu-id="5ce5b-132">c.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-132">c.</span></span>    <span data-ttu-id="5ce5b-133">您無法變更您要還原到 hello 共用 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-133">You cannot change hello type of hello share you are restoring to.</span></span> <span data-ttu-id="5ce5b-134">階層式共用會複製為階層式，固定在本機的共用則會還原為固定在本機。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-134">A tiered share is cloned as a tiered and a locally pinned share as locally pinned.</span></span>
   
   <span data-ttu-id="5ce5b-135">d.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-135">d.</span></span>    <span data-ttu-id="5ce5b-136">hello 容量設定為等於 toohello hello 您正在從複製的共用大小。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-136">hello capacity is set as equal toohello size of hello share you are cloning from.</span></span>
   
   <span data-ttu-id="5ce5b-137">e.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-137">e.</span></span>    <span data-ttu-id="5ce5b-138">指派此共用的 hello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-138">Assign hello administrators for this share.</span></span> <span data-ttu-id="5ce5b-139">Hello 複製完成之後，您將無法透過 [檔案總管] 可以 toomodify hello 共用屬性。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-139">You will be able toomodify hello share properties via File Explorer after hello clone is complete.</span></span>
   
   <span data-ttu-id="5ce5b-140">f.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-140">f.</span></span>    <span data-ttu-id="5ce5b-141">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-141">Click **OK**.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. <span data-ttu-id="5ce5b-143">按一下**複製**toostart 的複製工作。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-143">Click **Clone** toostart a clone job.</span></span> <span data-ttu-id="5ce5b-144">Hello 工作完成後，hello 複製作業開始，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-144">After hello job is complete, hello clone operation starts and you are notified.</span></span> <span data-ttu-id="5ce5b-145">複本上，移 toohello toomonitor hello 進度**作業**刀鋒視窗，然後按一下 hello 作業 tooview 工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-145">toomonitor hello progress of clone, go toohello **Jobs** blade and click hello job tooview job details.</span></span>
5. <span data-ttu-id="5ce5b-146">已成功建立 hello 複製之後，瀏覽後 toohello**共用**刀鋒視窗，在您的裝置上。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-146">After hello clone is successfully created, navigate back toohello **Shares** blade on your device.</span></span>
6. <span data-ttu-id="5ce5b-147">您現在可以檢視共用 hello 清單中的 hello 新複製的共用您的裝置上。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-147">You can now view hello new cloned share in hello list of shares on your device.</span></span> <span data-ttu-id="5ce5b-148">階層式共用會複製為階層式，固定在本機的共用則會複製為固定在本機的共用。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-148">A tiered share is cloned as tiered and a locally pinned share as a locally pinned share.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a><span data-ttu-id="5ce5b-150">從備份組複製磁碟區</span><span class="sxs-lookup"><span data-stu-id="5ce5b-150">Clone volumes from a backup set</span></span>

<span data-ttu-id="5ce5b-151">tooclone，從備份中 hello Azure 入口網站時，您有 tooperform 步驟類似 toohello 的複製共用。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-151">tooclone from a backup, in hello Azure portal, you have tooperform steps similar toohello ones when cloning a share.</span></span> <span data-ttu-id="5ce5b-152">hello 複製作業複製 hello 備份 tooa 新的磁碟區上 hello 相同的虛擬裝置。您無法再製 tooa 不同的裝置。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-152">hello clone operation clones hello backup tooa new volume on hello same virtual device; you cannot clone tooa different device.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="5ce5b-153">tooclone 磁碟區</span><span class="sxs-lookup"><span data-stu-id="5ce5b-153">tooclone a volume</span></span>

1. <span data-ttu-id="5ce5b-154">瀏覽過**裝置**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-154">Browse too**Devices** blade.</span></span> <span data-ttu-id="5ce5b-155">選取並按一下您的裝置，然後按一下磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-155">Select and click your device and then click **Volumes**.</span></span> <span data-ttu-id="5ce5b-156">選取您想 tooclone，以滑鼠右鍵按一下 hello 磁碟區 tooinvoke hello 內容功能表的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-156">Selec hello volume that you want tooclone, right-click hello volume tooinvoke hello context menu.</span></span> <span data-ttu-id="5ce5b-157">選取 [複製]。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-157">Select **Clone**.</span></span>
   
   ![複製磁碟區](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. <span data-ttu-id="5ce5b-159">在 hello**複製**刀鋒視窗中，按一下**備份**和執行然後 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5ce5b-159">In hello **Clone** blade, click **Backup** and then do hello following:</span></span> 
   
   <span data-ttu-id="5ce5b-160">a.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-160">a.</span></span>    <span data-ttu-id="5ce5b-161">篩選這個 hello 時間範圍為基礎的裝置上的備份。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-161">Filter a backup on this device based on hello time range.</span></span> <span data-ttu-id="5ce5b-162">您可以選擇 [過去 7 天]、[過去 30 天] 和 [過去一年]。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-162">You can choose from **Past 7 days**, **Past 30 days**, and **Past year**.</span></span> 
   
   <span data-ttu-id="5ce5b-163">b.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-163">b.</span></span>    <span data-ttu-id="5ce5b-164">Hello 在清單中顯示篩選過的備份，選取 從備份 tooclone。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-164">In hello list of filtered backups displayed, select a backup tooclone from.</span></span>
   
   <span data-ttu-id="5ce5b-165">c.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-165">c.</span></span>    <span data-ttu-id="5ce5b-166">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-166">Click **OK**.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. <span data-ttu-id="5ce5b-168">在 hello**複製**刀鋒視窗中，按一下**目標磁碟區設定**和執行然後 hello 遵循::</span><span class="sxs-lookup"><span data-stu-id="5ce5b-168">In hello **Clone** blade, click **Target volume settings** and then do hello following::</span></span>
   
   <span data-ttu-id="5ce5b-169">a.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-169">a.</span></span> <span data-ttu-id="5ce5b-170">自動填入 hello 裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-170">hello device name is automatically populated.</span></span>
   
   <span data-ttu-id="5ce5b-171">b.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-171">b.</span></span> <span data-ttu-id="5ce5b-172">提供磁碟區名稱 hello**複製磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-172">Provide a volume name for hello **cloned volume**.</span></span> <span data-ttu-id="5ce5b-173">hello 磁碟區名稱必須包含 3 too127 個字元。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-173">hello volume name must contain 3 too127 characters.</span></span>
   
   <span data-ttu-id="5ce5b-174">c.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-174">c.</span></span> <span data-ttu-id="5ce5b-175">hello 磁碟區類型會自動設定 toohello 原始磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-175">hello volume type is automatically set toohello original volume.</span></span> <span data-ttu-id="5ce5b-176">階層式磁碟區會複製為階層式，固定在本機的磁碟區則會複製為固定在本機。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-176">A tiered volume is cloned as tiered and a locally pinned volume as locally pinned.</span></span>
   
   <span data-ttu-id="5ce5b-177">d.</span><span class="sxs-lookup"><span data-stu-id="5ce5b-177">d.</span></span> <span data-ttu-id="5ce5b-178">Hello**連線主機**，按一下 **選取**。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-178">For hello **Connected hosts**, click **Select**.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. <span data-ttu-id="5ce5b-180">在 hello**連線主機**刀鋒視窗中，選取 從現有的 ACR，或加入新的 ACR。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-180">In  hello **Connected hosts** blade, select from an existing ACR or add a new ACR.</span></span> <span data-ttu-id="5ce5b-181">tooadd 新的 ACR，您將需要 tooprovide ACR 名稱和 hello 主機 IQN。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-181">tooadd a new ACR, you will need tooprovide an ACR name and hello host IQN.</span></span> <span data-ttu-id="5ce5b-182">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-182">Click **Select**.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. <span data-ttu-id="5ce5b-184">按一下**複製**toolaunch 的複製工作。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-184">Click **Clone** toolaunch a clone job.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. <span data-ttu-id="5ce5b-186">Hello 再製工作建立之後，複製會啟動。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-186">After hello clone job is created, cloning will start.</span></span> <span data-ttu-id="5ce5b-187">一旦建立 hello 複製時，它會顯示 hello 在裝置上的磁碟區 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-187">Once hello clone is created, it is displayed on hello Volumes blade on your device.</span></span> <span data-ttu-id="5ce5b-188">請注意，階層式磁碟區會複製為階層式，固定在本機的磁碟區則會複製為固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-188">Note that a tiered volume is cloned as tiered and a locally pinned volume is cloned as a locally pinned volume.</span></span>
   
   ![複製備份](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. <span data-ttu-id="5ce5b-190">Hello 磁碟區出現 online 上的磁碟區的 hello 清單時，hello 磁碟區是可供使用。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-190">Once hello volume appears online on hello list of volumes, hello volume is available for use.</span></span> <span data-ttu-id="5ce5b-191">Hello iSCSI 啟動器在主機上，重新整理 hello iSCSI 啟動器屬性 視窗中的目標清單。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-191">On hello iSCSI initiator host, refresh hello list of targets in iSCSI initiator properties window.</span></span> <span data-ttu-id="5ce5b-192">包含 hello 複製的磁碟區名稱的新目標應該為 'inactive' hello 狀態 欄位會出現。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-192">A new target that contains hello cloned volume name should appear as 'inactive' under hello status column.</span></span>
8. <span data-ttu-id="5ce5b-193">選取 hello 目標，然後按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-193">Select hello target and click **Connect**.</span></span> <span data-ttu-id="5ce5b-194">Hello 啟動器連接的 toohello 目標之後，hello 狀態應該變更太**Connected**。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-194">After hello initiator is connected toohello target, hello status should change too**Connected**.</span></span>
9. <span data-ttu-id="5ce5b-195">在 hello**磁碟管理**視窗中，hello 掛接的磁碟區會顯示 hello 下列圖例所示。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-195">In hello **Disk Management** window, hello mounted volumes appear as shown in hello following illustration.</span></span> <span data-ttu-id="5ce5b-196">以滑鼠右鍵按一下探索到的 hello 磁碟區 （按一下 hello 磁碟名稱），然後按一下**線上**。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-196">Right-click hello discovered volume (click hello disk name), and then click **Online**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ce5b-197">當嘗試 tooclone，磁碟區或共用從備份集，如果 hello 複製工作失敗、 目標磁碟區或共用仍可能在 hello 入口網站中建立。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-197">When trying tooclone a volume or a share from a backup set, if hello clone job fails, a target volume or share may still be created in hello portal.</span></span> <span data-ttu-id="5ce5b-198">請務必您刪除這個目標磁碟區或共用的 hello 入口 toominimize 從這個項目造成任何未來問題。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-198">It is important that you delete this target volume or share in hello portal toominimize any future issues arising from this element.</span></span>
> 
> 

## <a name="item-level-recovery-ilr"></a><span data-ttu-id="5ce5b-199">項目層級復原 (ILR)</span><span class="sxs-lookup"><span data-stu-id="5ce5b-199">Item-level recovery (ILR)</span></span>

<span data-ttu-id="5ce5b-200">此版本導入上設定為檔案伺服器的 StorSimple Virtual Array hello 項目層級復原 (ILR)。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-200">This release introduces hello item-level recovery (ILR) on a StorSimple Virtual Array configured as a file server.</span></span> <span data-ttu-id="5ce5b-201">hello 功能可讓您 toodo 的精細復原檔案和資料夾從雲端備份的所有 hello 共用 hello StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-201">hello feature allows you toodo granular recovery of files and folders from a cloud backup of all hello shares on hello StorSimple device.</span></span> <span data-ttu-id="5ce5b-202">您可以使用自助式模型，從最新的備份中擷取已刪除的檔案。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-202">You can retrieve deleted files from recent backups using a self-service model.</span></span>

<span data-ttu-id="5ce5b-203">每個共用*.backups*包含 hello 最新備份的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-203">Every share has a *.backups* folder that contains hello most recent backups.</span></span> <span data-ttu-id="5ce5b-204">您可以瀏覽 toohello 想要的備份、 複製相關的檔案和資料夾從 hello 備份和還原它們。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-204">You can navigate toohello desired backup, copy relevant files and folders from hello backup and restore them.</span></span> <span data-ttu-id="5ce5b-205">這項功能就不會呼叫 tooadministrators 從備份還原檔案。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-205">This feature eliminates calls tooadministrators for restoring files from backups.</span></span>

1. <span data-ttu-id="5ce5b-206">當執行 hello ILR，您可以檢視透過 [檔案總管] 中的 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-206">When performing hello ILR, you can view hello backups through File Explorer.</span></span> <span data-ttu-id="5ce5b-207">按一下您想要在 hello 備份 toolook hello 特定共用。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-207">Click hello specific share that you want toolook at hello backup for.</span></span> <span data-ttu-id="5ce5b-208">您會看到*.backups* hello 共用儲存所有 hello 備份之下建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-208">You will see a *.backups* folder created under hello share that stores all hello backups.</span></span> <span data-ttu-id="5ce5b-209">展開 hello *.backups*資料夾 tooview hello 備份。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-209">Expand hello *.backups* folder tooview hello backups.</span></span> <span data-ttu-id="5ce5b-210">hello 資料夾會顯示 hello hello 整個備份的階層式檢視。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-210">hello folder shows hello exploded view of hello entire backup hierarchy.</span></span> <span data-ttu-id="5ce5b-211">此檢視會建立依需求，並通常會採用只有少數幾秒 toocreate。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-211">This view is created on-demand and usually takes only a couple of seconds toocreate.</span></span>
   
   <span data-ttu-id="5ce5b-212">hello 最後五個備份以這種方式顯示，而且可以是使用的 tooperform 項目層級復原。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-212">hello last five backups are displayed in this way and can be used tooperform an item-level recovery.</span></span> <span data-ttu-id="5ce5b-213">hello 五個最新備份同時包含 hello 預設的排程和 hello 手動備份。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-213">hello five recent backups include both hello default scheduled and hello manual backups.</span></span>
   
   * <span data-ttu-id="5ce5b-214">**排程備份**，命名為 &lt;裝置名稱&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-214">**Scheduled backups** named as &lt;Device name&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC.</span></span>
   * <span data-ttu-id="5ce5b-215">**手動備份** ，命名為 Ad-hoc-YYYYMMDD-HHMMSS-UTC。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-215">**Manual backups** named as Ad-hoc-YYYYMMDD-HHMMSS-UTC.</span></span>
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. <span data-ttu-id="5ce5b-216">識別 hello 備份，其中包含 hello hello 刪除檔案的最新的版本。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-216">Identify hello backup containing hello most recent version of hello deleted file.</span></span> <span data-ttu-id="5ce5b-217">雖然 hello 資料夾名稱包含 UTC 時間戳記在每個 hello 上述情況下，建立資料夾的哪些 hello hello 時間會是 hello 實際裝置 hello 備份開始的時間。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-217">Though hello folder name contains a UTC timestamp in each of hello preceding cases, hello time at which hello folder was created is hello actual device time when hello backup started.</span></span> <span data-ttu-id="5ce5b-218">使用 hello 資料夾時間戳記 toolocate，並找出 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-218">Use hello folder timestamp toolocate and identify hello backups.</span></span>

3. <span data-ttu-id="5ce5b-219">找出 hello 資料夾或您想在 hello 備份您所識別的 toorestore hello 上一個步驟中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-219">Locate hello folder or hello file that you want toorestore in hello backup that you identified in hello previous step.</span></span> <span data-ttu-id="5ce5b-220">請注意，您只能檢視 hello 檔案或資料夾的擁有權限。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-220">Note you can only view hello files or folders that you have permissions for.</span></span> <span data-ttu-id="5ce5b-221">如果您無法存取某些檔案或資料夾，請連絡共用系統管理員。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-221">If you cannot access certain files or folders, contact a share administrator.</span></span> <span data-ttu-id="5ce5b-222">hello 系統管理員可以使用檔案總管 tooedit hello 共用權限，並可讓您存取 toohello 特定檔案或資料夾。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-222">hello administrator can use File Explorer tooedit hello share permissions and give you access toohello specific file or folder.</span></span> <span data-ttu-id="5ce5b-223">它是建議的最佳作法 hello 共用系統管理員的使用者群組，而不是單一使用者。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-223">It is a recommended best practice that hello share administrator is a user group instead of a single user.</span></span>

4. <span data-ttu-id="5ce5b-224">複製 hello 檔案或 hello 資料夾 toohello 適當的共用您的 StorSimple 檔案伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-224">Copy hello file or hello folder toohello appropriate share on your StorSimple file server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ce5b-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ce5b-225">Next steps</span></span>

<span data-ttu-id="5ce5b-226">深入了解如何太[管理使用本機 web UI hello 您 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="5ce5b-226">Learn more about how too[administer your StorSimple Virtual Array using hello local web UI](storsimple-ova-web-ui-admin.md).</span></span>

