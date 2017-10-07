---
title: "aaaStorSimple Snapshot Manager 備份類別目錄 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooview 和管理 hello 備份類別目錄。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a><span data-ttu-id="1986e-103">使用 StorSimple Snapshot Manager toomanage hello 備份類別目錄</span><span class="sxs-lookup"><span data-stu-id="1986e-103">Use StorSimple Snapshot Manager toomanage hello backup catalog</span></span>

## <a name="overview"></a><span data-ttu-id="1986e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1986e-104">Overview</span></span>
<span data-ttu-id="1986e-105">hello 主要函式的 StorSimple Snapshot Manager 是的 tooallow 您 toocreate 應用程式一致備份複本的快照集的 hello 形式的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-105">hello primary function of StorSimple Snapshot Manager is tooallow you toocreate application-consistent backup copies of StorSimple volumes in hello form of snapshots.</span></span> <span data-ttu-id="1986e-106">快照集會列在稱為 *備份目錄*的 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1986e-106">Snapshots are then listed in an XML file called a *backup catalog*.</span></span> <span data-ttu-id="1986e-107">hello 備份類別目錄會組織依磁碟區群組及本機快照或雲端快照的快照集。</span><span class="sxs-lookup"><span data-stu-id="1986e-107">hello backup catalog organizes snapshots by volume group and then by local snapshot or cloud snapshot.</span></span>

<span data-ttu-id="1986e-108">這個教學課程描述如何使用 hello**備份類別目錄**節點 toocomplete hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="1986e-108">This tutorial describes how you can use hello **Backup Catalog** node toocomplete hello following tasks:</span></span>

* <span data-ttu-id="1986e-109">還原磁碟區</span><span class="sxs-lookup"><span data-stu-id="1986e-109">Restore a volume</span></span>
* <span data-ttu-id="1986e-110">複製磁碟區或磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="1986e-110">Clone a volume or volume group</span></span>
* <span data-ttu-id="1986e-111">刪除備份</span><span class="sxs-lookup"><span data-stu-id="1986e-111">Delete a backup</span></span>
* <span data-ttu-id="1986e-112">復原檔案</span><span class="sxs-lookup"><span data-stu-id="1986e-112">Recover a file</span></span>
* <span data-ttu-id="1986e-113">還原 hello Storsimple Snapshot Manager 資料庫</span><span class="sxs-lookup"><span data-stu-id="1986e-113">Restore hello Storsimple Snapshot Manager database</span></span>

<span data-ttu-id="1986e-114">您可以檢視 hello 備份類別目錄的展開 hello**備份類別目錄**節點 hello**範圍**窗格中，然後再展開 hello 磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="1986e-114">You can view hello backup catalog by expanding hello **Backup Catalog** node in hello **Scope** pane, and then expanding hello volume group.</span></span>

* <span data-ttu-id="1986e-115">如果您按一下 hello 磁碟區群組名稱，hello**結果** 窗格會顯示 hello 本機快照及雲端快照可用於 hello 磁碟區群組數目。</span><span class="sxs-lookup"><span data-stu-id="1986e-115">If you click hello volume group name, hello **Results** pane shows hello number of local snapshots and cloud snapshots available for hello volume group.</span></span> 
* <span data-ttu-id="1986e-116">如果您按一下**本機快照**或**雲端快照**，hello**結果** 窗格會顯示下列每個備份快照的相關資訊的 hello (根據您**檢視**設定):</span><span class="sxs-lookup"><span data-stu-id="1986e-116">If you click **Local Snapshot** or **Cloud Snapshot**, hello **Results** pane shows hello following information about each backup snapshot (depending on your **View** settings):</span></span>
  
  * <span data-ttu-id="1986e-117">**名稱**– hello 時間 hello 快照。</span><span class="sxs-lookup"><span data-stu-id="1986e-117">**Name** – hello time hello snapshot was taken.</span></span>
  * <span data-ttu-id="1986e-118">**類型** – 這是本機快照集或雲端快照集。</span><span class="sxs-lookup"><span data-stu-id="1986e-118">**Type** – whether this is a local snapshot or a cloud snapshot.</span></span>
  * <span data-ttu-id="1986e-119">**擁有者**– hello 內容擁有者。</span><span class="sxs-lookup"><span data-stu-id="1986e-119">**Owner** – hello content owner.</span></span> 
  * <span data-ttu-id="1986e-120">**可用**– 是否 hello 快照集是目前可用。</span><span class="sxs-lookup"><span data-stu-id="1986e-120">**Available** – whether hello snapshot is currently available.</span></span> <span data-ttu-id="1986e-121">**True**表示該 hello 快照集為可用，且可加以還原;**False**指出該 hello 快照集已無法再使用。</span><span class="sxs-lookup"><span data-stu-id="1986e-121">**True** indicates that hello snapshot is available and can be restored; **False** indicates that hello snapshot is no longer available.</span></span> 
  * <span data-ttu-id="1986e-122">**匯入**– 是否已匯入 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="1986e-122">**Imported** – whether hello backup was imported.</span></span> <span data-ttu-id="1986e-123">**True**指出 hello StorSimple 裝置管理員在 hello 時間 hello 裝置上的服務未設定 StorSimple Snapshot Manager 中; 從匯入該 hello 備份**False**表示它未匯入，但 StorSimple Snapshot Manager 所建立。</span><span class="sxs-lookup"><span data-stu-id="1986e-123">**True** indicates that hello backup was imported from hello StorSimple Device Manager service at hello time hello device was configured in StorSimple Snapshot Manager; **False** indicates that it was not imported, but was created by StorSimple Snapshot Manager.</span></span> <span data-ttu-id="1986e-124">（您可以輕鬆地識別匯入的磁碟區群組因為可識別 hello 裝置 hello 磁碟區群組匯入的新增後置字元。）</span><span class="sxs-lookup"><span data-stu-id="1986e-124">(You can easily identify an imported volume group because a suffix is added that identifies hello device from which hello volume group was imported.)</span></span>
    
    ![備份類別目錄](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* <span data-ttu-id="1986e-126">如果您展開**本機快照**或**雲端快照**，然後按一下個別快照名稱，hello**結果** 窗格會顯示下列資訊 hello hello您選取的快照集：</span><span class="sxs-lookup"><span data-stu-id="1986e-126">If you expand **Local Snapshot** or **Cloud Snapshot**, and then click an individual snapshot name, hello **Results** pane shows hello following information about hello snapshot that you selected:</span></span>
  
  * <span data-ttu-id="1986e-127">**名稱**– hello 根據磁碟機代號的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-127">**Name** – hello volume identified by drive letter.</span></span> 
  * <span data-ttu-id="1986e-128">**本機名稱**– hello hello 磁碟機 （如果有的話） 的本機名稱。</span><span class="sxs-lookup"><span data-stu-id="1986e-128">**Local Name** – hello local name of hello drive (if available).</span></span> 
  * <span data-ttu-id="1986e-129">**裝置**– hello hello 裝置的 hello 所在磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="1986e-129">**Device** – hello name of hello device on which hello volume resides.</span></span> 
  * <span data-ttu-id="1986e-130">**可用**– 是否 hello 快照集是目前可用。</span><span class="sxs-lookup"><span data-stu-id="1986e-130">**Available** – whether hello snapshot is currently available.</span></span> <span data-ttu-id="1986e-131">**True**表示該 hello 快照集為可用，且可加以還原;**False**指出該 hello 快照集已無法再使用。</span><span class="sxs-lookup"><span data-stu-id="1986e-131">**True** indicates that hello snapshot is available and can be restored; **False** indicates that hello snapshot is no longer available.</span></span> 

## <a name="restore-a-volume"></a><span data-ttu-id="1986e-132">還原磁碟區</span><span class="sxs-lookup"><span data-stu-id="1986e-132">Restore a volume</span></span>
<span data-ttu-id="1986e-133">使用下列程序 toorestore 磁碟區從備份中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1986e-133">Use hello following procedure toorestore a volume from backup.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="1986e-134">必要條件</span><span class="sxs-lookup"><span data-stu-id="1986e-134">Prerequisites</span></span>
<span data-ttu-id="1986e-135">如果您尚未這樣做，請建立磁碟區和磁碟區群組，然後再刪除 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-135">If you have not already done so, create a volume and volume group, and then delete hello volume.</span></span> <span data-ttu-id="1986e-136">根據預設，StorSimple Snapshot Manager 備份磁碟區之前允許它 toobe 刪除。</span><span class="sxs-lookup"><span data-stu-id="1986e-136">By default, StorSimple Snapshot Manager backs up a volume before permitting it toobe deleted.</span></span> <span data-ttu-id="1986e-137">如果不小心刪除 hello 磁碟區，或需要復原，因為任何原因 toobe hello 資料，這樣的預防措施可以防止資料遺失。</span><span class="sxs-lookup"><span data-stu-id="1986e-137">This precaution can prevent data loss if hello volume is deleted unintentionally or if hello data needs toobe recovered for any reason.</span></span> 

<span data-ttu-id="1986e-138">StorSimple Snapshot Manager 顯示 hello 下會在建立 hello 預防備份時的訊息。</span><span class="sxs-lookup"><span data-stu-id="1986e-138">StorSimple Snapshot Manager displays hello following message while it creates hello precautionary backup.</span></span>

![自動快照訊息](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> <span data-ttu-id="1986e-140">您無法刪除磁碟區，因為它是磁碟區群組的一部分的。</span><span class="sxs-lookup"><span data-stu-id="1986e-140">You cannot delete a volume that is part of a volume group.</span></span> <span data-ttu-id="1986e-141">hello 刪除選項無法使用。</span><span class="sxs-lookup"><span data-stu-id="1986e-141">hello delete option is unavailable.</span></span> <br>
> 
> 

#### <a name="toorestore-a-volume"></a><span data-ttu-id="1986e-142">toorestore 磁碟區</span><span class="sxs-lookup"><span data-stu-id="1986e-142">toorestore a volume</span></span>
1. <span data-ttu-id="1986e-143">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="1986e-143">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="1986e-144">在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**] 節點，展開 [磁碟區群組，然後按一下**本機快照**或**雲端快照**.</span><span class="sxs-lookup"><span data-stu-id="1986e-144">In hello **Scope** pane, expand hello **Backup Catalog** node, expand a volume group, and then click **Local Snapshots** or **Cloud Snapshots**.</span></span> <span data-ttu-id="1986e-145">備份快照清單會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="1986e-145">A list of backup snapshots appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="1986e-146">Toorestore、 按一下滑鼠右鍵，然後再按一下您要尋找 hello 備份**還原**。</span><span class="sxs-lookup"><span data-stu-id="1986e-146">Find hello backup that you want toorestore, right-click, and then click **Restore**.</span></span>
   
    ![還原備份目錄](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. <span data-ttu-id="1986e-148">在 hello 確認頁面上，檢閱 hello 的詳細資訊，請輸入**確認**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1986e-148">On hello confirmation page, review hello details, type **Confirm**, and then click **OK**.</span></span> <span data-ttu-id="1986e-149">StorSimple Snapshot Manager 會使用 hello 備份 toorestore hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-149">StorSimple Snapshot Manager uses hello backup toorestore hello volume.</span></span>
   
    ![還原確認訊息](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. <span data-ttu-id="1986e-151">當它執行時，您可以監視 hello 還原動作。</span><span class="sxs-lookup"><span data-stu-id="1986e-151">You can monitor hello restore action as it runs.</span></span> <span data-ttu-id="1986e-152">在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後再按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="1986e-152">In hello **Scope** pane, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="1986e-153">hello 工作詳細資料會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="1986e-153">hello job details appear in hello **Results** pane.</span></span> <span data-ttu-id="1986e-154">Hello 工作詳細資料 hello 還原作業完成時，會傳送的 toohello**過去 24 小時**清單。</span><span class="sxs-lookup"><span data-stu-id="1986e-154">When hello restore job is finished, hello job details are transferred toohello **Last 24 hours** list.</span></span>

## <a name="clone-a-volume-or-volume-group"></a><span data-ttu-id="1986e-155">複製磁碟區或磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="1986e-155">Clone a volume or volume group</span></span>
<span data-ttu-id="1986e-156">使用下列程序 toocreate 磁碟區或磁碟區群組的複本 （副本） hello。</span><span class="sxs-lookup"><span data-stu-id="1986e-156">Use hello following procedure toocreate a duplicate (clone) of a volume or volume group.</span></span>

#### <a name="tooclone-a-volume-or-volume-group"></a><span data-ttu-id="1986e-157">tooclone 磁碟區或磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="1986e-157">tooclone a volume or volume group</span></span>
1. <span data-ttu-id="1986e-158">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="1986e-158">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1986e-159">在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**] 節點，展開 [磁碟區群組，然後按一下**雲端快照**。</span><span class="sxs-lookup"><span data-stu-id="1986e-159">In hello **Scope** pane, expand hello **Backup Catalog** node, expand a volume group, and then click **Cloud Snapshots**.</span></span> <span data-ttu-id="1986e-160">備份清單會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="1986e-160">A list of backups appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="1986e-161">尋找 hello 磁碟區或磁碟區群組，您想 tooclone、 以滑鼠右鍵按一下 hello 磁碟區或磁碟區群組名稱，然後按一下 **複製**。</span><span class="sxs-lookup"><span data-stu-id="1986e-161">Find hello volume or volume group that you want tooclone, right-click hello volume or volume group name, and click **Clone**.</span></span> <span data-ttu-id="1986e-162">hello**複製雲端快照** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1986e-162">hello **Clone Cloud Snapshot** dialog box appears.</span></span>
   
    ![複製雲端快照集](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. <span data-ttu-id="1986e-164">完整的 hello**複製雲端快照**對話方塊中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1986e-164">Complete hello **Clone Cloud Snapshot** dialog box as follows:</span></span> 
   
   1. <span data-ttu-id="1986e-165">在 [hello**名稱**] 文字方塊中，輸入的名稱 hello 複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-165">In hello **Name** text box, type a name for hello cloned volume.</span></span> <span data-ttu-id="1986e-166">這個名稱會出現在 hello**磁碟區**節點。</span><span class="sxs-lookup"><span data-stu-id="1986e-166">This name will appear in hello **Volumes** node.</span></span> 
   2. <span data-ttu-id="1986e-167">（選擇性） 選取**磁碟機**，然後從 hello 下拉式清單中選取磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="1986e-167">(Optional) select **Drive**, and then select a drive letter from hello drop-down list.</span></span>
   3. <span data-ttu-id="1986e-168">（選擇性） 選取**資料夾 (NTFS)**，並輸入資料夾路徑，或按一下 瀏覽並選取 hello 資料夾位置。</span><span class="sxs-lookup"><span data-stu-id="1986e-168">(Optional) select **Folder (NTFS)**, and type a folder path or click Browse and select a location for hello folder.</span></span> 
   4. <span data-ttu-id="1986e-169">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1986e-169">Click **Create**.</span></span>
5. <span data-ttu-id="1986e-170">Hello 複製程序完成時，您必須先初始化 hello 複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-170">When hello cloning process is finished, you must initialize hello cloned volume.</span></span> <span data-ttu-id="1986e-171">啟動伺服器管理員，然後啟動磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="1986e-171">Start Server Manager, and then start Disk Management.</span></span> <span data-ttu-id="1986e-172">如需詳細指示，請參閱 [掛接磁碟區](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)。</span><span class="sxs-lookup"><span data-stu-id="1986e-172">For detailed instructions, see [Mount volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes).</span></span> <span data-ttu-id="1986e-173">在初始化之後，將列 hello 磁碟區之下 hello**磁碟區**hello 節點**範圍**窗格。</span><span class="sxs-lookup"><span data-stu-id="1986e-173">After it is initialized, hello volume will be listed under hello **Volumes** node in hello **Scope** pane.</span></span> <span data-ttu-id="1986e-174">如果看不到 hello 磁碟區列出，請重新整理的磁碟區的 hello 清單 (以滑鼠右鍵按一下 hello**磁碟區**節點，然後再按一下**重新整理**)。</span><span class="sxs-lookup"><span data-stu-id="1986e-174">If you do not see hello volume listed, refresh hello list of volumes (right-click hello **Volumes** node, and then click **Refresh**).</span></span>

## <a name="delete-a-backup"></a><span data-ttu-id="1986e-175">刪除備份</span><span class="sxs-lookup"><span data-stu-id="1986e-175">Delete a backup</span></span>
<span data-ttu-id="1986e-176">使用 hello hello 備份類別目錄中的下列程序 toodelete 快照集。</span><span class="sxs-lookup"><span data-stu-id="1986e-176">Use hello following procedure toodelete a snapshot from hello backup catalog.</span></span> 

> [!NOTE]
> <span data-ttu-id="1986e-177">刪除快照會刪除 hello 備份 hello 快照集相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="1986e-177">Deleting a snapshot deletes hello backed up data associated with hello snapshot.</span></span> <span data-ttu-id="1986e-178">不過，hello 的從 hello 雲端清除資料的程序可能需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="1986e-178">However, hello process of cleaning up data from hello cloud may take some time.</span></span><br>


#### <a name="toodelete-a-backup"></a><span data-ttu-id="1986e-179">toodelete 備份</span><span class="sxs-lookup"><span data-stu-id="1986e-179">toodelete a backup</span></span>
1. <span data-ttu-id="1986e-180">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="1986e-180">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="1986e-181">在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**] 節點，展開 [磁碟區群組，然後按一下**本機快照**或**雲端快照**.</span><span class="sxs-lookup"><span data-stu-id="1986e-181">In hello **Scope** pane, expand hello **Backup Catalog** node, expand a volume group, and then click **Local Snapshots** or **Cloud Snapshots**.</span></span> <span data-ttu-id="1986e-182">快照清單會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="1986e-182">A list of snapshots appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="1986e-183">以滑鼠右鍵按一下您想 toodelete，然後再按一下 hello 快照**刪除**。</span><span class="sxs-lookup"><span data-stu-id="1986e-183">Right-click hello snapshot you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="1986e-184">Hello 確認訊息出現時，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="1986e-184">When hello confirmation message appears, click **OK**.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="1986e-185">復原檔案</span><span class="sxs-lookup"><span data-stu-id="1986e-185">Recover a file</span></span>
<span data-ttu-id="1986e-186">如果不小心刪除檔案時從磁碟區，您可以藉由擷取預先日期 hello 刪除、 使用 hello 快照 toocreate 的快照集的 hello 大量複製復原 hello 檔案，然後複製從 hello 檔案 hello 複製的磁碟區 toohello 原始磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-186">If a file is accidentally deleted from a volume, you can recover hello file by retrieving a snapshot that pre-dates hello deletion, using hello snapshot toocreate a clone of hello volume, and then copying hello file from hello cloned volume toohello original volume.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="1986e-187">必要條件</span><span class="sxs-lookup"><span data-stu-id="1986e-187">Prerequisites</span></span>
<span data-ttu-id="1986e-188">在開始之前，請確定您擁有 hello 磁碟區群組的目前備份。</span><span class="sxs-lookup"><span data-stu-id="1986e-188">Before you begin, make sure that you have a current backup of hello volume group.</span></span> <span data-ttu-id="1986e-189">然後，刪除儲存在其中一個該磁碟區群組中的 hello 磁碟區上的檔案。</span><span class="sxs-lookup"><span data-stu-id="1986e-189">Then, delete a file stored on one of hello volumes in that volume group.</span></span> <span data-ttu-id="1986e-190">最後，使用您的備份中的下列步驟 toorestore hello 刪除檔案的 hello。</span><span class="sxs-lookup"><span data-stu-id="1986e-190">Finally, use hello following steps toorestore hello deleted file from your backup.</span></span> 

#### <a name="toorecover-a-deleted-file"></a><span data-ttu-id="1986e-191">toorecover 已刪除的檔案</span><span class="sxs-lookup"><span data-stu-id="1986e-191">toorecover a deleted file</span></span>
1. <span data-ttu-id="1986e-192">按一下桌面上的 hello StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="1986e-192">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="1986e-193">hello StorSimple Snapshot Manager 主控台 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1986e-193">hello StorSimple Snapshot Manager console window appears.</span></span> 
2. <span data-ttu-id="1986e-194">在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**節點，然後瀏覽 tooa 快照集，其中包含 hello 刪除檔案。</span><span class="sxs-lookup"><span data-stu-id="1986e-194">In hello **Scope** pane, expand hello **Backup Catalog** node, and browse tooa snapshot that contains hello deleted file.</span></span> <span data-ttu-id="1986e-195">一般而言，您應該選取 hello 刪除之前建立的快照集。</span><span class="sxs-lookup"><span data-stu-id="1986e-195">Typically, you should select a snapshot that was created just before hello deletion.</span></span>
3. <span data-ttu-id="1986e-196">您想 tooclone，按一下滑鼠右鍵，然後按一下 尋找 hello 磁碟區**複製**。</span><span class="sxs-lookup"><span data-stu-id="1986e-196">Find hello volume that you want tooclone, right-click, and click **Clone**.</span></span> <span data-ttu-id="1986e-197">hello**複製雲端快照** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1986e-197">hello **Clone Cloud Snapshot** dialog box appears.</span></span>
   
    ![複製雲端快照集](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. <span data-ttu-id="1986e-199">完整的 hello**複製雲端快照**對話方塊中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1986e-199">Complete hello **Clone Cloud Snapshot** dialog box as follows:</span></span> 
   
   1. <span data-ttu-id="1986e-200">在 [hello**名稱**] 文字方塊中，輸入的名稱 hello 複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-200">In hello **Name** text box, type a name for hello cloned volume.</span></span> <span data-ttu-id="1986e-201">這個名稱會出現在 hello**磁碟區**節點。</span><span class="sxs-lookup"><span data-stu-id="1986e-201">This name will appear in hello **Volumes** node.</span></span> 
   2. <span data-ttu-id="1986e-202">（選擇性）選取**磁碟機**，然後從 hello 下拉式清單中選取磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="1986e-202">(Optional) Select **Drive**, and then select a drive letter from hello drop-down list.</span></span> 
   3. <span data-ttu-id="1986e-203">（選擇性）選取**資料夾 (NTFS)**，然後輸入資料夾路徑，或按一下**瀏覽**選取 hello 資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="1986e-203">(Optional) Select **Folder (NTFS)**, and type a folder path or click **Browse** and select a location for hello folder.</span></span> 
   4. <span data-ttu-id="1986e-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1986e-204">Click **Create**.</span></span> 
5. <span data-ttu-id="1986e-205">Hello 複製程序完成時，您必須先初始化 hello 複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-205">When hello cloning process is finished, you must initialize hello cloned volume.</span></span> <span data-ttu-id="1986e-206">啟動伺服器管理員，然後啟動磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="1986e-206">Start Server Manager, and then start Disk Management.</span></span> <span data-ttu-id="1986e-207">如需詳細指示，請參閱 [掛接磁碟區](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)。</span><span class="sxs-lookup"><span data-stu-id="1986e-207">For detailed instructions, see [Mount volumes](storsimple-snapshot-manager-manage-volumes.md#mount-volumes).</span></span> <span data-ttu-id="1986e-208">在初始化之後，將列 hello 磁碟區之下 hello**磁碟區**hello 節點**範圍**窗格。</span><span class="sxs-lookup"><span data-stu-id="1986e-208">After it is initialized, hello volume will be listed under hello **Volumes** node in hello **Scope** pane.</span></span> 
   
    <span data-ttu-id="1986e-209">如果看不到 hello 磁碟區列出，請重新整理的磁碟區的 hello 清單 (以滑鼠右鍵按一下 hello**磁碟區**節點，然後再按一下**重新整理**)。</span><span class="sxs-lookup"><span data-stu-id="1986e-209">If you do not see hello volume listed, refresh hello list of volumes (right-click hello **Volumes** node, and then click **Refresh**).</span></span>
6. <span data-ttu-id="1986e-210">開啟 hello NTFS 資料夾包含 hello 複製磁碟區，展開 hello**磁碟區**節點，然後再開啟 hello 複製磁碟區。</span><span class="sxs-lookup"><span data-stu-id="1986e-210">Open hello NTFS folder that contains hello cloned volume, expand hello **Volumes** node, and then open hello cloned volume.</span></span> <span data-ttu-id="1986e-211">尋找您想 toorecover，並將它複製 toohello 主要磁碟區的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1986e-211">Find hello file that you want toorecover, and copy it toohello primary volume.</span></span>
7. <span data-ttu-id="1986e-212">還原 hello 檔案之後，您可以刪除 hello 包含 hello 複製磁碟區的 NTFS 資料夾。</span><span class="sxs-lookup"><span data-stu-id="1986e-212">After you restore hello file, you can delete hello NTFS folder that contains hello cloned volume.</span></span>

## <a name="restore-hello-storsimple-snapshot-manager-database"></a><span data-ttu-id="1986e-213">還原 hello StorSimple Snapshot Manager 資料庫</span><span class="sxs-lookup"><span data-stu-id="1986e-213">Restore hello StorSimple Snapshot Manager database</span></span>
<span data-ttu-id="1986e-214">您應該定期備份 hello hello 主機電腦上的 StorSimple Snapshot Manager 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1986e-214">You should regularly back up hello StorSimple Snapshot Manager database on hello host computer.</span></span> <span data-ttu-id="1986e-215">如果發生損毀或因任何原因失敗 hello 主機電腦，然後可以將它從 hello 備份中還原。</span><span class="sxs-lookup"><span data-stu-id="1986e-215">If a disaster occurs or hello host computer fails for any reason, you can then restore it from hello backup.</span></span> <span data-ttu-id="1986e-216">建立 hello 資料庫備份是手動程序。</span><span class="sxs-lookup"><span data-stu-id="1986e-216">Creating hello database backup is a manual process.</span></span>

#### <a name="tooback-up-and-restore-hello-database"></a><span data-ttu-id="1986e-217">向上 tooback 和還原 hello 資料庫</span><span class="sxs-lookup"><span data-stu-id="1986e-217">tooback up and restore hello database</span></span>
1. <span data-ttu-id="1986e-218">停止 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="1986e-218">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="1986e-219">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="1986e-219">Start Server Manager.</span></span>
   2. <span data-ttu-id="1986e-220">Hello 伺服器管理員儀表板上，在 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="1986e-220">On hello Server Manager dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="1986e-221">在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="1986e-221">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="1986e-222">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。</span><span class="sxs-lookup"><span data-stu-id="1986e-222">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
2. <span data-ttu-id="1986e-223">Hello 主機電腦上，瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="1986e-223">On hello host computer, browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1986e-224">ProgramData 是隱藏的資料夾。</span><span class="sxs-lookup"><span data-stu-id="1986e-224">ProgramData is a hidden folder.</span></span>
   > 
   > 
3. <span data-ttu-id="1986e-225">尋找 hello 類別目錄 XML 檔案，複製 hello 檔案，並存放區 hello 複製在安全的位置或 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="1986e-225">Find hello catalog XML file, copy hello file, and store hello copy in a safe location or in hello cloud.</span></span> <span data-ttu-id="1986e-226">如果 hello 主機失敗，您可以使用這個備份檔案 toohelp 復原 hello 備份原則建立 StorSimple Snapshot Manager 中。</span><span class="sxs-lookup"><span data-stu-id="1986e-226">If hello host fails, you can use this backup file toohelp recover hello backup policies that you created in StorSimple Snapshot Manager.</span></span>
   
    ![Azure StorSimple 備份目錄檔案](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. <span data-ttu-id="1986e-228">重新啟動 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="1986e-228">Restart hello Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="1986e-229">Hello 伺服器管理員儀表板上，在 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="1986e-229">On hello Server Manager dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="1986e-230">在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="1986e-230">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="1986e-231">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="1986e-231">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span>
5. <span data-ttu-id="1986e-232">Hello 主機電腦上，瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="1986e-232">On hello host computer, browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
6. <span data-ttu-id="1986e-233">刪除 hello 類別目錄 XML 檔案，然後 hello 您所建立的備份版本取代它。</span><span class="sxs-lookup"><span data-stu-id="1986e-233">Delete hello catalog XML file, and replace it with hello backup version that you created.</span></span> 
7. <span data-ttu-id="1986e-234">按一下桌面 StorSimple Snapshot Manager 圖示 toostart hello StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="1986e-234">Click hello desktop StorSimple Snapshot Manager icon toostart StorSimple Snapshot Manager.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1986e-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1986e-235">Next steps</span></span>
* <span data-ttu-id="1986e-236">深入了解[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="1986e-236">Learn more about [using StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="1986e-237">深入了解 [StorSimple Snapshot Manager 工作和工作流程](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows)。</span><span class="sxs-lookup"><span data-stu-id="1986e-237">Learn more about [StorSimple Snapshot Manager tasks and workflows](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).</span></span>

