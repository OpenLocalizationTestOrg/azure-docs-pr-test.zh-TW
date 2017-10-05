---
title: "StorSimple Snapshot Manager 磁碟區群組 | Microsoft Docs"
description: "描述如何使用 StorSimple Snapshot Manager MMC 嵌入式管理單元，來建立和理磁碟區群組。"
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
ms.openlocfilehash: 6067a88cd42d29c3d2f4b74580095424de77561e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="19ceb-103">使用 StorSimple Snapshot Manager 來建立和管理磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="19ceb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="19ceb-104">Overview</span></span>
<span data-ttu-id="19ceb-105">您可以使用 [範圍] 窗格上的 [磁碟區群組] 節點，將磁碟區指派給磁碟區群組、檢視磁碟區群組的相關資訊、排定備份，以及編輯磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="19ceb-106">磁碟區群組是用來確保應用程式具有一致備份之相關磁碟區的集區。</span><span class="sxs-lookup"><span data-stu-id="19ceb-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="19ceb-107">如需詳細資訊，請參閱[磁碟區和磁碟區群組](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups)，以及[與 Windows 磁碟區陰影複製服務整合](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)。</span><span class="sxs-lookup"><span data-stu-id="19ceb-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="19ceb-108">磁碟區群組中的所有磁碟區必須來自單一雲端服務提供者。</span><span class="sxs-lookup"><span data-stu-id="19ceb-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="19ceb-109">當設定磁碟區群組時，請勿在相同的磁碟區群組中混用叢集共用磁碟區 (CSV) 和非 CSV。</span><span class="sxs-lookup"><span data-stu-id="19ceb-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="19ceb-110">StorSimple Snapshot Manager 不支援在相同快照中混用 CSV 和非 CSV。</span><span class="sxs-lookup"><span data-stu-id="19ceb-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>

![磁碟區群組節點](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="19ceb-112">**圖 1：StorSimple Snapshot Manager 磁碟區群組節點**</span><span class="sxs-lookup"><span data-stu-id="19ceb-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="19ceb-113">本教學課程說明如何使用 StorSimple Snapshot Manager：</span><span class="sxs-lookup"><span data-stu-id="19ceb-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="19ceb-114">檢視磁碟區群組的相關資訊</span><span class="sxs-lookup"><span data-stu-id="19ceb-114">View information about your volume groups</span></span>
* <span data-ttu-id="19ceb-115">建立磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-115">Create a volume group</span></span>
* <span data-ttu-id="19ceb-116">備份磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-116">Back up a volume group</span></span>
* <span data-ttu-id="19ceb-117">編輯磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-117">Edit a volume group</span></span>
* <span data-ttu-id="19ceb-118">刪除磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-118">Delete a volume group</span></span>

<span data-ttu-id="19ceb-119">所有這些動作也可在 [動作]  窗格上進行。</span><span class="sxs-lookup"><span data-stu-id="19ceb-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="19ceb-120">檢視磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-120">View volume groups</span></span>
<span data-ttu-id="19ceb-121">如果您按一下 [磁碟區群組] 節點，[結果] 窗格會顯示每個磁碟區群組的下列相關資訊，視您選擇的資料行而定。</span><span class="sxs-lookup"><span data-stu-id="19ceb-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="19ceb-122">您可以設定 [結果] 窗格中的資料行。</span><span class="sxs-lookup"><span data-stu-id="19ceb-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="19ceb-123">(以滑鼠右鍵按一下 [磁碟區] 節點，選取 [檢視]，然後選取 [新增/移除資料行]。)</span><span class="sxs-lookup"><span data-stu-id="19ceb-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="19ceb-124">結果資料行</span><span class="sxs-lookup"><span data-stu-id="19ceb-124">Results column</span></span> | <span data-ttu-id="19ceb-125">說明</span><span class="sxs-lookup"><span data-stu-id="19ceb-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="19ceb-126">名稱</span><span class="sxs-lookup"><span data-stu-id="19ceb-126">Name</span></span> |<span data-ttu-id="19ceb-127">[名稱]  資料行包含磁碟區群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="19ceb-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="19ceb-128">應用程式</span><span class="sxs-lookup"><span data-stu-id="19ceb-128">Application</span></span> |<span data-ttu-id="19ceb-129">[應用程式]  資料行會顯示 Windows 主機上目前已安裝且正在執行的 VSS 寫入器數目。</span><span class="sxs-lookup"><span data-stu-id="19ceb-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="19ceb-130">已選取</span><span class="sxs-lookup"><span data-stu-id="19ceb-130">Selected</span></span> |<span data-ttu-id="19ceb-131">[已選取]  資料行會顯示磁碟區群組中所包含的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="19ceb-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="19ceb-132">零 (0) 表示沒有任何應用程式與磁碟區群組中的磁碟區相關聯。</span><span class="sxs-lookup"><span data-stu-id="19ceb-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="19ceb-133">已匯入</span><span class="sxs-lookup"><span data-stu-id="19ceb-133">Imported</span></span> |<span data-ttu-id="19ceb-134">[已匯入] 資料行會顯示已匯入的磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="19ceb-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="19ceb-135">當設定為 **True** 時，此資料行會指出已從 Azure 入口網站匯入磁碟區群組，而不是在 StorSimple Snapshot Manager 中建立它。</span><span class="sxs-lookup"><span data-stu-id="19ceb-135">When set to **True**, this column indicates that a volume group was imported from the Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="19ceb-136">StorSimple Snapshot Manager 磁碟區群組也會顯示在 Azure 入口網站的 [備份原則] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="19ceb-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="19ceb-137">建立磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-137">Create a volume group</span></span>
<span data-ttu-id="19ceb-138">請使用下列程序來建立磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="19ceb-139">若要建立磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-139">To create a volume group</span></span>
1. <span data-ttu-id="19ceb-140">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="19ceb-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="19ceb-141">在 [範圍] 窗格中，以滑鼠右鍵按一下 [磁碟區群組]，然後按一下 [建立磁碟區群組]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![建立磁碟區群組](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="19ceb-143">[建立磁碟區群組]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="19ceb-143">The **Create a volume group** dialog box appears.</span></span>
   
    ![建立磁碟區群組對話方塊](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="19ceb-145">輸入以下資訊：</span><span class="sxs-lookup"><span data-stu-id="19ceb-145">Enter the following information:</span></span>
   
   1. <span data-ttu-id="19ceb-146">在 [名稱]  方塊中，輸入新的磁碟區群組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="19ceb-146">In the **Name** box, type a unique name for the new volume group.</span></span>
   2. <span data-ttu-id="19ceb-147">在 [應用程式]  方塊中，選取與您將新增至磁碟區群組之磁碟區相關聯的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19ceb-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span>
      
       <span data-ttu-id="19ceb-148">[應用程式]  方塊僅會列出那些使用 StorSimple 磁碟區，並對它們啟用 VSS 寫入器的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19ceb-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="19ceb-149">只在寫入器注意的所有磁碟區都是 StorSimple 磁碟區時，才會啟用 VSS 寫入器。</span><span class="sxs-lookup"><span data-stu-id="19ceb-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="19ceb-150">如果 [應用程式] 方塊是空的，則不會安裝任何使用 Azure StorSimple 磁碟區，並具有支援之 VSS 寫入器的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19ceb-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="19ceb-151">(目前，Azure StorSimple 支援 Microsoft Exchange 和 SQL Server)。如需 VSS 寫入器的詳細資訊，請參閱[與 Windows 磁碟區陰影複製服務整合](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)。</span><span class="sxs-lookup"><span data-stu-id="19ceb-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="19ceb-152">如果選取應用程式，則會自動選取所有與其相關聯的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="19ceb-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="19ceb-153">相反地，如果選取與特定應用程式相關聯的磁碟區，則會在 [應用程式]  方塊中自動選取該應用程式。</span><span class="sxs-lookup"><span data-stu-id="19ceb-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="19ceb-154">在 [磁碟區]  方塊中，選取要新增到磁碟區群組的 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="19ceb-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="19ceb-155">您可以包含具有單一或多個磁碟分割的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="19ceb-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="19ceb-156">(多個磁碟分割磁碟區可以是具有多個磁碟分割的動態磁碟或基本磁碟)。包含多個磁碟分割的磁碟區會被視為單一單位。</span><span class="sxs-lookup"><span data-stu-id="19ceb-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="19ceb-157">因此，如果您只將其中一個磁碟分割新增到磁碟區群組，則所有其他磁碟分割會同時自動新增到該磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="19ceb-158">在將多個磁碟分割磁碟區新增到磁碟區群組之後，多個磁碟分割磁碟區會繼續被視為單一單位。</span><span class="sxs-lookup"><span data-stu-id="19ceb-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="19ceb-159">您可以建立空的磁碟區群組，方法是不將任何磁碟區指派給它們。</span><span class="sxs-lookup"><span data-stu-id="19ceb-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="19ceb-160">請勿在相同的磁碟區群組中混用叢集共用磁碟區 (CSV) 和非 CSV。</span><span class="sxs-lookup"><span data-stu-id="19ceb-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="19ceb-161">StorSimple Snapshot Manager 不支援在相同快照中混用 CSV 磁碟區和非 CSV 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="19ceb-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span>
4. <span data-ttu-id="19ceb-162">按一下 [確定]  儲存磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="19ceb-163">備份磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-163">Back up a volume group</span></span>
<span data-ttu-id="19ceb-164">請使用下列程序來備份磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="19ceb-165">若要備份磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-165">To back up a volume group</span></span>
1. <span data-ttu-id="19ceb-166">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="19ceb-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="19ceb-167">在 [範圍] 窗格中，展開 [磁碟區群組] 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後按一下 [取得備份]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![立即備份磁碟區群組](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="19ceb-169">在 [取得備份] 對話方塊中，選取 [本機快照] 或 [雲端快照]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![取得備份對話方塊](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="19ceb-171">若要確認備份執行中，請展開 [作業] 節點，然後按一下 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="19ceb-172">應該會列出備份。</span><span class="sxs-lookup"><span data-stu-id="19ceb-172">The backup should be listed.</span></span>
5. <span data-ttu-id="19ceb-173">若要檢視已完成的快照集，請展開 [備份目錄] 節點，展開磁碟區群組名稱，然後按一下 [本機快照] 或 [雲端快照]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="19ceb-174">如果順利完成，將會列出備份。</span><span class="sxs-lookup"><span data-stu-id="19ceb-174">The backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="19ceb-175">編輯磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-175">Edit a volume group</span></span>
<span data-ttu-id="19ceb-176">請使用下列程序來編輯磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="19ceb-177">若要編輯磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-177">To edit a volume group</span></span>
1. <span data-ttu-id="19ceb-178">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="19ceb-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="19ceb-179">在 [範圍] 窗格中，展開 [磁碟區群組] 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後按一下 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="19ceb-180">[建立磁碟區群組] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="19ceb-180">The **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="19ceb-181">您可以變更 [名稱]、[應用程式] 和 [磁碟區] 項目。</span><span class="sxs-lookup"><span data-stu-id="19ceb-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="19ceb-182">按一下 [確定]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="19ceb-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="19ceb-183">刪除磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-183">Delete a volume group</span></span>
<span data-ttu-id="19ceb-184">請使用下列程序來刪除磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="19ceb-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="19ceb-185">這也會刪除所有與磁碟區群組相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="19ceb-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="19ceb-186">若要刪除磁碟區群組</span><span class="sxs-lookup"><span data-stu-id="19ceb-186">To delete a volume group</span></span>
1. <span data-ttu-id="19ceb-187">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="19ceb-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="19ceb-188">在 [範圍] 窗格中，展開 [磁碟區群組] 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="19ceb-189">[刪除磁碟區群組] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="19ceb-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="19ceb-190">在文字方塊中輸入 **Confirm**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="19ceb-190">Type **Confirm** in the text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="19ceb-191">刪除的磁碟區群組會從 [結果]  窗格中的清單消失，而且所有與該磁碟區群組相關聯的備份都會從備份目錄中刪除。</span><span class="sxs-lookup"><span data-stu-id="19ceb-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19ceb-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="19ceb-192">Next steps</span></span>
* <span data-ttu-id="19ceb-193">了解如何 [使用 StorSimple Snapshot Manager 來管理您的 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="19ceb-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="19ceb-194">了解如何 [使用 StorSimple Snapshot Manager 建立和管理備份原則](storsimple-snapshot-manager-manage-backup-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="19ceb-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

