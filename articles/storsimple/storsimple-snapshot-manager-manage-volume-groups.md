---
title: "aaaStorSimple Snapshot Manager 磁碟區群組 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 toocreate 和管理磁碟區群組。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a><span data-ttu-id="43c7e-103">使用 StorSimple Snapshot Manager toocreate 及管理磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-103">Use StorSimple Snapshot Manager toocreate and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="43c7e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="43c7e-104">Overview</span></span>
<span data-ttu-id="43c7e-105">您可以使用 hello**磁碟區群組**節點上 hello**範圍**窗格 tooassign 磁碟區 toovolume 群組，檢視資訊的磁碟區群組，排程備份，並編輯磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="43c7e-105">You can use hello **Volume Groups** node on hello **Scope** pane tooassign volumes toovolume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="43c7e-106">磁碟區群組是使用相關的磁碟區 tooensure 備份是應用程式一致的集區。</span><span class="sxs-lookup"><span data-stu-id="43c7e-106">Volume groups are pools of related volumes used tooensure that backups are application-consistent.</span></span> <span data-ttu-id="43c7e-107">如需詳細資訊，請參閱[磁碟區和磁碟區群組](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups)，以及[與 Windows 磁碟區陰影複製服務整合](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)。</span><span class="sxs-lookup"><span data-stu-id="43c7e-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="43c7e-108">磁碟區群組中的所有磁碟區必須來自單一雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="43c7e-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="43c7e-109">當您設定磁碟區群組時，請勿混用叢集共用磁碟區 (Csv) 和非 Csv hello 中相同的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="43c7e-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="43c7e-110">StorSimple Snapshot Manager 不支援混用 Csv 和非 Csv 中 hello 相同的快照集。</span><span class="sxs-lookup"><span data-stu-id="43c7e-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in hello same snapshot.</span></span>

![磁碟區群組節點](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="43c7e-112">**圖 1：StorSimple Snapshot Manager 磁碟區群組節點**</span><span class="sxs-lookup"><span data-stu-id="43c7e-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="43c7e-113">本教學課程說明如何使用 StorSimple Snapshot Manager：</span><span class="sxs-lookup"><span data-stu-id="43c7e-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="43c7e-114">檢視磁碟區群組的相關資訊</span><span class="sxs-lookup"><span data-stu-id="43c7e-114">View information about your volume groups</span></span>
* <span data-ttu-id="43c7e-115">建立磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-115">Create a volume group</span></span>
* <span data-ttu-id="43c7e-116">備份磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-116">Back up a volume group</span></span>
* <span data-ttu-id="43c7e-117">編輯磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-117">Edit a volume group</span></span>
* <span data-ttu-id="43c7e-118">刪除磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-118">Delete a volume group</span></span>

<span data-ttu-id="43c7e-119">所有這些動作也會提供在 hello**動作**窗格。</span><span class="sxs-lookup"><span data-stu-id="43c7e-119">All of these actions are also available on hello **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="43c7e-120">檢視磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-120">View volume groups</span></span>
<span data-ttu-id="43c7e-121">如果您按一下 hello**磁碟區群組**節點、 hello**結果** 窗格會顯示 hello 下列每個磁碟區群組的相關資訊，請根據 hello 資料行的選項。</span><span class="sxs-lookup"><span data-stu-id="43c7e-121">If you click hello **Volume Groups** node, hello **Results** pane shows hello following information about each volume group, depending on hello column selections you make.</span></span> <span data-ttu-id="43c7e-122">(hello hello 中的資料行**結果**窗格可加以設定。</span><span class="sxs-lookup"><span data-stu-id="43c7e-122">(hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="43c7e-123">以滑鼠右鍵按一下 hello**磁碟區**節點中，選取**檢視**，然後選取**新增/移除欄位**。)</span><span class="sxs-lookup"><span data-stu-id="43c7e-123">Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="43c7e-124">結果資料行</span><span class="sxs-lookup"><span data-stu-id="43c7e-124">Results column</span></span> | <span data-ttu-id="43c7e-125">說明</span><span class="sxs-lookup"><span data-stu-id="43c7e-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="43c7e-126">名稱</span><span class="sxs-lookup"><span data-stu-id="43c7e-126">Name</span></span> |<span data-ttu-id="43c7e-127">hello**名稱**資料行包含 hello hello 磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="43c7e-127">hello **Name** column contains hello name of hello volume group.</span></span> |
| <span data-ttu-id="43c7e-128">應用程式</span><span class="sxs-lookup"><span data-stu-id="43c7e-128">Application</span></span> |<span data-ttu-id="43c7e-129">hello**應用程式**欄顯示 hello 號碼目前已安裝的 VSS 寫入器和上執行 hello Windows 主機。</span><span class="sxs-lookup"><span data-stu-id="43c7e-129">hello **Applications** column shows hello number of VSS writers currently installed and running on hello Windows host.</span></span> |
| <span data-ttu-id="43c7e-130">已選取</span><span class="sxs-lookup"><span data-stu-id="43c7e-130">Selected</span></span> |<span data-ttu-id="43c7e-131">hello**選取**資料行會顯示 hello 磁碟區群組中所包含的磁碟區的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="43c7e-131">hello **Selected** column shows hello number of volumes that are contained in hello volume group.</span></span> <span data-ttu-id="43c7e-132">零 (0) 表示沒有任何應用程式都與 hello hello 磁碟區群組中的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43c7e-132">A zero (0) indicates that no application is associated with hello volumes in hello volume group.</span></span> |
| <span data-ttu-id="43c7e-133">已匯入</span><span class="sxs-lookup"><span data-stu-id="43c7e-133">Imported</span></span> |<span data-ttu-id="43c7e-134">hello**已匯入**資料行會顯示 hello 匯入的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="43c7e-134">hello **Imported** column shows hello number of imported volumes.</span></span> <span data-ttu-id="43c7e-135">當設定太**True**，此資料行表示磁碟區群組從 hello Azure 入口網站匯入，而且未建立 StorSimple Snapshot Manager 中。</span><span class="sxs-lookup"><span data-stu-id="43c7e-135">When set too**True**, this column indicates that a volume group was imported from hello Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="43c7e-136">StorSimple Snapshot Manager 磁碟區群組也會顯示在 hello**備份原則**hello Azure 入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="43c7e-136">StorSimple Snapshot Manager volume groups are also displayed on hello **Backup Policies** tab in hello Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="43c7e-137">建立磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-137">Create a volume group</span></span>
<span data-ttu-id="43c7e-138">使用下列程序 toocreate 磁碟區群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="43c7e-138">Use hello following procedure toocreate a volume group.</span></span>

#### <a name="toocreate-a-volume-group"></a><span data-ttu-id="43c7e-139">toocreate 磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-139">toocreate a volume group</span></span>
1. <span data-ttu-id="43c7e-140">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="43c7e-140">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43c7e-141">在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**磁碟區群組**，然後按一下**建立磁碟區群組**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-141">In hello **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![建立磁碟區群組](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="43c7e-143">hello**建立磁碟區群組** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="43c7e-143">hello **Create a volume group** dialog box appears.</span></span>
   
    ![建立磁碟區群組對話方塊](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="43c7e-145">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="43c7e-145">Enter hello following information:</span></span>
   
   1. <span data-ttu-id="43c7e-146">在 hello**名稱**方塊中，輸入 hello 新磁碟區群組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="43c7e-146">In hello **Name** box, type a unique name for hello new volume group.</span></span>
   2. <span data-ttu-id="43c7e-147">在 hello**應用程式**方塊中，選取與 hello 磁碟區，您會將加入 toohello 磁碟區群組相關聯的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43c7e-147">In hello **Applications** box, select applications associated with hello volumes that you will be adding toohello volume group.</span></span>
      
       <span data-ttu-id="43c7e-148">hello**應用程式** 方塊中列出的那些應用程式使用 StorSimple 磁碟區且具有 VSS 寫入器啟用它們。</span><span class="sxs-lookup"><span data-stu-id="43c7e-148">hello **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="43c7e-149">VSS 寫入器已啟用，只有在所有 hello 磁碟區 hello 寫入器注意的是 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43c7e-149">A VSS writer is enabled only if all hello volumes that hello writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="43c7e-150">如果 hello 應用程式 方塊是空的然後才會不安裝任何應用程式，使用 Azure StorSimple 磁碟區，並支援 VSS 寫入器。</span><span class="sxs-lookup"><span data-stu-id="43c7e-150">If hello Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="43c7e-151">(目前，Azure StorSimple 支援 Microsoft Exchange 和 SQL Server)。如需 VSS 寫入器的詳細資訊，請參閱[與 Windows 磁碟區陰影複製服務整合](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)。</span><span class="sxs-lookup"><span data-stu-id="43c7e-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="43c7e-152">如果選取應用程式，則會自動選取所有與其相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43c7e-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="43c7e-153">相反地，如果您選取特定的應用程式相關聯的磁碟區，hello 應用程式中自動選取 hello**應用程式**方塊。</span><span class="sxs-lookup"><span data-stu-id="43c7e-153">Conversely, if you select volumes associated with a specific application, hello application is automatically selected in hello **Applications** box.</span></span> 
   3. <span data-ttu-id="43c7e-154">在 hello**磁碟區**方塊中，選取 StorSimple 磁碟區 tooadd toohello 磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="43c7e-154">In hello **Volumes** box, select StorSimple volumes tooadd toohello volume group.</span></span> 
      
      * <span data-ttu-id="43c7e-155">您可以包含具有單一或多個磁碟分割的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="43c7e-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="43c7e-156">(多個磁碟分割磁碟區可以是具有多個磁碟分割的動態磁碟或基本磁碟)。包含多個磁碟分割的磁碟區會被視為單一單位。</span><span class="sxs-lookup"><span data-stu-id="43c7e-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="43c7e-157">因此，如果您將其中一個 hello 分割 tooa 磁碟區群組，所有的 hello 加入了其他資料分割會自動新增的 toothat 磁碟區群組在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="43c7e-157">Consequently, if you add only one of hello partitions tooa volume group, all hello other partitions are automatically added toothat volume group at hello same time.</span></span> <span data-ttu-id="43c7e-158">您加入多個資料分割的磁碟區 tooa 磁碟區群組之後，hello 多個磁碟分割磁碟區會繼續 toobe 當做單一單位來處理。</span><span class="sxs-lookup"><span data-stu-id="43c7e-158">After you add a multiple partition volume tooa volume group, hello multiple partition volume continues toobe treated as a single unit.</span></span>
      * <span data-ttu-id="43c7e-159">您可以建立空的磁碟區群組未指派任何磁碟區 toothem。</span><span class="sxs-lookup"><span data-stu-id="43c7e-159">You can create empty volume groups by not assigning any volumes toothem.</span></span> 
      * <span data-ttu-id="43c7e-160">請勿混用叢集共用磁碟區 (Csv) 和非 Csv hello 中相同的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="43c7e-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="43c7e-161">StorSimple Snapshot Manager 不支援混用 CSV 磁碟區和非 CSV 磁碟區中的 hello 相同的快照集。</span><span class="sxs-lookup"><span data-stu-id="43c7e-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in hello same snapshot.</span></span>
4. <span data-ttu-id="43c7e-162">按一下**確定**toosave hello 磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="43c7e-162">Click **OK** toosave hello volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="43c7e-163">備份磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-163">Back up a volume group</span></span>
<span data-ttu-id="43c7e-164">使用下列程序 tooback 磁碟區群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="43c7e-164">Use hello following procedure tooback up a volume group.</span></span>

#### <a name="tooback-up-a-volume-group"></a><span data-ttu-id="43c7e-165">tooback 磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-165">tooback up a volume group</span></span>
1. <span data-ttu-id="43c7e-166">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="43c7e-166">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43c7e-167">在 hello**範圍** 窗格中，展開 hello**磁碟區群組** 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後**取得備份**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-167">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![立即備份磁碟區群組](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="43c7e-169">在 hello**取得備份**對話方塊中，選取**本機快照**或**雲端快照**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-169">In hello **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![取得備份對話方塊](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="43c7e-171">hello 備份的 tooconfirm 正在執行中，展開 hello**作業**節點，然後再按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-171">tooconfirm that hello backup is running, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="43c7e-172">應該會列出 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="43c7e-172">hello backup should be listed.</span></span>
5. <span data-ttu-id="43c7e-173">tooview hello 完成快照集，請展開 hello**備份類別目錄** 節點，展開 hello 磁碟區群組名稱，然後按一下**本機快照**或**雲端快照**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-173">tooview hello completed snapshot, expand hello **Backup Catalog** node, expand hello volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="43c7e-174">如果它已順利完成，將會列出 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="43c7e-174">hello backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="43c7e-175">編輯磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-175">Edit a volume group</span></span>
<span data-ttu-id="43c7e-176">使用下列程序 tooedit 磁碟區群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="43c7e-176">Use hello following procedure tooedit a volume group.</span></span>

#### <a name="tooedit-a-volume-group"></a><span data-ttu-id="43c7e-177">tooedit 磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-177">tooedit a volume group</span></span>
1. <span data-ttu-id="43c7e-178">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="43c7e-178">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43c7e-179">在 hello**範圍** 窗格中，展開 hello**磁碟區群組** 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後**編輯**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-179">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="43c7e-180">hello * * 建立磁碟區群組 * * 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="43c7e-180">hello **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="43c7e-181">您可以變更 hello**名稱**，**應用程式**，和**磁碟區**項目。</span><span class="sxs-lookup"><span data-stu-id="43c7e-181">You can change hello **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="43c7e-182">按一下**確定**toosave 您的變更。</span><span class="sxs-lookup"><span data-stu-id="43c7e-182">Click **OK** toosave your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="43c7e-183">刪除磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-183">Delete a volume group</span></span>
<span data-ttu-id="43c7e-184">使用下列程序 toodelete 磁碟區群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="43c7e-184">Use hello following procedure toodelete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="43c7e-185">這也會刪除所有與 hello 磁碟區群組相關聯的 hello 備份。</span><span class="sxs-lookup"><span data-stu-id="43c7e-185">This also deletes all hello backups associated with hello volume group.</span></span>
> 
> 

#### <a name="toodelete-a-volume-group"></a><span data-ttu-id="43c7e-186">toodelete 磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="43c7e-186">toodelete a volume group</span></span>
1. <span data-ttu-id="43c7e-187">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="43c7e-187">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="43c7e-188">在 hello**範圍** 窗格中，展開 hello**磁碟區群組** 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後**刪除**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-188">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="43c7e-189">hello**刪除磁碟區群組** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="43c7e-189">hello **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="43c7e-190">型別**確認**在 hello 文字方塊中，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="43c7e-190">Type **Confirm** in hello text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="43c7e-191">從在 hello hello 清單消失 hello 刪除磁碟區群組**結果**窗格和與該磁碟區群組相關聯的所有備份都會從 hello 備份類別目錄刪除。</span><span class="sxs-lookup"><span data-stu-id="43c7e-191">hello deleted volume group vanishes from hello list in hello **Results** pane and all backups that are associated with that volume group are deleted from hello backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43c7e-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43c7e-192">Next steps</span></span>
* <span data-ttu-id="43c7e-193">了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="43c7e-193">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="43c7e-194">了解如何太[使用 StorSimple Snapshot Manager toocreate 及管理備份原則](storsimple-snapshot-manager-manage-backup-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="43c7e-194">Learn how too[use StorSimple Snapshot Manager toocreate and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

