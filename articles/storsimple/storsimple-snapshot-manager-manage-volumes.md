---
title: "StorSimple Snapshot Manager 及磁碟區 | Microsoft Docs"
description: "描述如何使用 StorSimple Snapshot Manager MMC 嵌入式管理單元來檢視和管理磁碟區及設定備份。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 2c0b211bced99d272a73a7b018a22f99d8d58aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-volumes"></a><span data-ttu-id="0a219-103">使用 StorSimple Snapshot Manager 來檢視和管理磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-103">Use StorSimple Snapshot Manager to view and manage volumes</span></span>
## <a name="overview"></a><span data-ttu-id="0a219-104">概觀</span><span class="sxs-lookup"><span data-stu-id="0a219-104">Overview</span></span>
<span data-ttu-id="0a219-105">您可以使用 StorSimple Snapshot Manager 的 [磁碟區] 節點 (在 [範圍] 窗格上)，選取磁碟區並檢視其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0a219-105">You can use the StorSimple Snapshot Manager **Volumes** node (on the **Scope** pane) to select volumes and view information about them.</span></span> <span data-ttu-id="0a219-106">磁碟區會呈現為對應至主機所掛接磁碟區的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="0a219-106">The volumes are presented as drives that correspond to the volumes mounted by the host.</span></span> <span data-ttu-id="0a219-107">[磁碟區]  節點會顯示 StorSimple 所支援的本機磁碟區和磁碟區類型，包括透過使用 iSCSI 及裝置探索到的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-107">The **Volumes** node shows local volumes and volume types that are supported by StorSimple, including volumes discovered through the use of iSCSI and a device.</span></span> 

<span data-ttu-id="0a219-108">如需支援之磁碟區的詳細資訊，請移至《 [支援多個磁碟區類型](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types)》。</span><span class="sxs-lookup"><span data-stu-id="0a219-108">For more information about supported volumes, go to [Support for multiple volume types](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).</span></span>

![在 [結果] 窗格中的磁碟區清單](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

<span data-ttu-id="0a219-110">[磁碟區]  節點也可讓您在 StorSimple Snapshot Manager 探索到磁碟區之後，重新掃描或刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-110">The **Volumes** node also lets you rescan or delete volumes after StorSimple Snapshot Manager discovers them.</span></span> 

<span data-ttu-id="0a219-111">本教學課程說明如何掛載、初始化和格式化磁碟區，然後使用 StorSimple Snapshot Manager：</span><span class="sxs-lookup"><span data-stu-id="0a219-111">This tutorial explains how you can mount, initialize, and format volumes and then use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="0a219-112">檢視磁碟區的相關資訊</span><span class="sxs-lookup"><span data-stu-id="0a219-112">View information about volumes</span></span> 
* <span data-ttu-id="0a219-113">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-113">Delete volumes</span></span>
* <span data-ttu-id="0a219-114">重新掃描磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-114">Rescan volumes</span></span> 
* <span data-ttu-id="0a219-115">設定基本磁碟區並將其備份</span><span class="sxs-lookup"><span data-stu-id="0a219-115">Configure a basic volume and back it up</span></span>
* <span data-ttu-id="0a219-116">設定動態鏡像磁碟區並將其備份</span><span class="sxs-lookup"><span data-stu-id="0a219-116">Configure a dynamic mirrored volume and back it up</span></span>

> [!NOTE]
> <span data-ttu-id="0a219-117">所有 [磁碟區] 節點動作也可以在 [動作] 窗格中取得。</span><span class="sxs-lookup"><span data-stu-id="0a219-117">All of the **Volume** node actions are also available in the **Actions** pane.</span></span>
> 
> 

## <a name="mount-volumes"></a><span data-ttu-id="0a219-118">掛接磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-118">Mount volumes</span></span>
<span data-ttu-id="0a219-119">請使用下列程序，來掛接、初始化和格式化 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-119">Use the following procedure to mount, initialize, and format StorSimple volumes.</span></span> <span data-ttu-id="0a219-120">此程序使用 [磁碟管理]，這是一種系統公用程式，用於管理硬碟及其相對應的磁碟區或磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="0a219-120">This procedure uses Disk Management, a system utility for managing hard disks and the corresponding volumes or partitions.</span></span> <span data-ttu-id="0a219-121">如需 [磁碟管理] 的詳細資訊，請移至 Microsoft TechNet 網站上的 [磁碟管理](https://technet.microsoft.com/library/cc770943.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="0a219-121">For more information about Disk Management, go to [Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on the Microsoft TechNet website.</span></span>

#### <a name="to-mount-volumes"></a><span data-ttu-id="0a219-122">若要掛接磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-122">To mount volumes</span></span>
1. <span data-ttu-id="0a219-123">在您的主機電腦上，啟動 Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="0a219-123">On your host computer, start the Microsoft iSCSI initiator.</span></span>
2. <span data-ttu-id="0a219-124">提供其中一個介面 IP 位址作為目標入口網站，或探索 IP 位址，然後連接至裝置。</span><span class="sxs-lookup"><span data-stu-id="0a219-124">Supply one of the interface IP addresses as the target portal or discovery IP address, and connect to the device.</span></span> <span data-ttu-id="0a219-125">在連接裝置之後，您的 Windows 系統將可存取磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-125">After the device is connected, the volumes will be accessible to your Windows system.</span></span> <span data-ttu-id="0a219-126">如需使用 Microsoft iSCSI 啟動器的詳細資訊，請移至[安裝和設定 Microsoft iSCSI 啟動器][1]中的〈連接至 iSCSI 目標裝置〉一節。</span><span class="sxs-lookup"><span data-stu-id="0a219-126">For more information about using the Microsoft iSCSI initiator, go to the section “Connecting to an iSCSI target device” in [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
3. <span data-ttu-id="0a219-127">請使用下列任一個選項來啟動 [磁碟管理]：</span><span class="sxs-lookup"><span data-stu-id="0a219-127">Use any of the following options to start Disk Management:</span></span>
   
   * <span data-ttu-id="0a219-128">在 [執行]  方塊中輸入 Diskmgmt.msc。</span><span class="sxs-lookup"><span data-stu-id="0a219-128">Type Diskmgmt.msc in the **Run** box.</span></span>
   * <span data-ttu-id="0a219-129">啟動 [伺服器管理員]，展開 [儲存體] 節點，然後選取 [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="0a219-129">Start Server Manager, expand the **Storage** node, and then select **Disk Management**.</span></span>
   * <span data-ttu-id="0a219-130">啟動 [系統管理工具]，展開 [電腦管理] 節點，然後選取 [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="0a219-130">Start **Administrative Tools**, expand the **Computer Management** node, and then select **Disk Management**.</span></span> 
     
     > [!NOTE]
     > <span data-ttu-id="0a219-131">您必須使用系統管理員權限，才能執行 [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="0a219-131">You must use administrator privileges to run Disk Management.</span></span>
     > 
     > 
4. <span data-ttu-id="0a219-132">將磁碟區連線：</span><span class="sxs-lookup"><span data-stu-id="0a219-132">Take the volume(s) online:</span></span>
   
   1. <span data-ttu-id="0a219-133">在 [磁碟管理] 中，以滑鼠右鍵按一下任何標示為 [離線] 的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-133">In Disk Management, right-click any volume marked **Offline**.</span></span>
   2. <span data-ttu-id="0a219-134">按一下 [重新啟動磁碟] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-134">Click **Reactivate Disk**.</span></span> <span data-ttu-id="0a219-135">磁碟重新啟動之後，應該標示為 [線上]  。</span><span class="sxs-lookup"><span data-stu-id="0a219-135">The disk should be marked **Online** after the disk is reactivated.</span></span>
5. <span data-ttu-id="0a219-136">初始化磁碟區：</span><span class="sxs-lookup"><span data-stu-id="0a219-136">Initialize the volume(s):</span></span>
   
   1. <span data-ttu-id="0a219-137">以滑鼠右鍵按一下已探索到的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-137">Right-click the discovered volumes.</span></span>
   2. <span data-ttu-id="0a219-138">在功能表上，選取 [初始化磁碟] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-138">On the menu, select **Initialize Disk**.</span></span>
   3. <span data-ttu-id="0a219-139">在 [初始化磁碟] 對話方塊中，選取您要初始化的磁碟，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0a219-139">In the **Initialize Disk** dialog box, select the disks that you want to initialize, and then click **OK**.</span></span>
6. <span data-ttu-id="0a219-140">格式化簡單磁碟區：</span><span class="sxs-lookup"><span data-stu-id="0a219-140">Format simple volumes:</span></span>
   
   1. <span data-ttu-id="0a219-141">以滑鼠右鍵按一下您想要格式化的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-141">Right-click a volume that you want to format.</span></span>
   2. <span data-ttu-id="0a219-142">在功能表上，選取 [新增簡單磁碟區] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-142">On the menu, select **New Simple Volume**.</span></span>
   3. <span data-ttu-id="0a219-143">使用 [新增簡單磁碟區] 精靈來格式化磁碟區：</span><span class="sxs-lookup"><span data-stu-id="0a219-143">Use the New Simple Volume wizard to format the volume:</span></span>
      
      * <span data-ttu-id="0a219-144">指定磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="0a219-144">Specify the volume size.</span></span>
      * <span data-ttu-id="0a219-145">提供磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="0a219-145">Supply a drive letter.</span></span>
      * <span data-ttu-id="0a219-146">選取 NTFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="0a219-146">Select the NTFS file system.</span></span>
      * <span data-ttu-id="0a219-147">指定 64 KB 的配置單位大小。</span><span class="sxs-lookup"><span data-stu-id="0a219-147">Specify a 64 KB allocation unit size.</span></span>
      * <span data-ttu-id="0a219-148">執行快速格式化。</span><span class="sxs-lookup"><span data-stu-id="0a219-148">Perform a quick format.</span></span>
7. <span data-ttu-id="0a219-149">格式化多重磁碟分割磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-149">Format multi-partition volumes.</span></span> <span data-ttu-id="0a219-150">如需指示，請移至《 [實作磁碟管理](https://msdn.microsoft.com/library/dd163556.aspx)》的〈磁碟分割與磁碟區〉一節。</span><span class="sxs-lookup"><span data-stu-id="0a219-150">For instructions, go to the section, "Partitions and Volumes" in [Implementing Disk Management](https://msdn.microsoft.com/library/dd163556.aspx).</span></span>

## <a name="view-information-about-your-volumes"></a><span data-ttu-id="0a219-151">檢視您磁碟區的相關資訊</span><span class="sxs-lookup"><span data-stu-id="0a219-151">View information about your volumes</span></span>
<span data-ttu-id="0a219-152">請使用下列程序，來檢視本機和 Azure StorSimple 磁碟區的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0a219-152">Use the following procedure to view information about local and Azure StorSimple volumes.</span></span>

#### <a name="to-view-volume-information"></a><span data-ttu-id="0a219-153">若要檢視磁碟區資訊</span><span class="sxs-lookup"><span data-stu-id="0a219-153">To view volume information</span></span>
1. <span data-ttu-id="0a219-154">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0a219-154">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="0a219-155">在 [範圍] 窗格中，按一下 [磁碟區] 節點。</span><span class="sxs-lookup"><span data-stu-id="0a219-155">In the **Scope** pane, click the **Volumes** node.</span></span> <span data-ttu-id="0a219-156">本機與掛接的磁碟區 (包括所有的 Azure StorSimple 磁碟區) 的清單會出現在 [結果] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="0a219-156">A list of local and mounted volumes, including all Azure StorSimple volumes, appears in the **Results** pane.</span></span> <span data-ttu-id="0a219-157">您可以設定 [結果] 窗格中的資料行。</span><span class="sxs-lookup"><span data-stu-id="0a219-157">The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="0a219-158">(以滑鼠右鍵按一下 [磁碟區] 節點，選取 [檢視]，然後選取 [新增/移除資料行]。)</span><span class="sxs-lookup"><span data-stu-id="0a219-158">(Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>
   
    ![設定資料行](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | <span data-ttu-id="0a219-160">結果資料行</span><span class="sxs-lookup"><span data-stu-id="0a219-160">Results column</span></span> | <span data-ttu-id="0a219-161">說明</span><span class="sxs-lookup"><span data-stu-id="0a219-161">Description</span></span> |
   |:--- |:--- |
   |  <span data-ttu-id="0a219-162">名稱</span><span class="sxs-lookup"><span data-stu-id="0a219-162">Name</span></span> |<span data-ttu-id="0a219-163">[名稱]  資料行包含已指派至每個已探索到之磁碟區的磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="0a219-163">The **Name** column contains the drive letter assigned to each discovered volume.</span></span> |
   |  <span data-ttu-id="0a219-164">裝置</span><span class="sxs-lookup"><span data-stu-id="0a219-164">Device</span></span> |<span data-ttu-id="0a219-165">[裝置]  資料行包含已連接到主機電腦之裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0a219-165">The **Device** column contains the IP address of the device connected to the host computer.</span></span> |
   |  <span data-ttu-id="0a219-166">裝置磁碟區名稱</span><span class="sxs-lookup"><span data-stu-id="0a219-166">Device Volume Name</span></span> |<span data-ttu-id="0a219-167">[裝置磁碟區名稱]  資料行包含所選磁碟區所屬之裝置磁碟區的名稱。</span><span class="sxs-lookup"><span data-stu-id="0a219-167">The **Device Volume Name** column contains the name of the device volume to which the selected volume belongs.</span></span> <span data-ttu-id="0a219-168">這是 Azure 入口網站中針對該特定磁碟區定義的磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="0a219-168">This is the volume name defined in the Azure portal for that specific volume.</span></span> |
   |  <span data-ttu-id="0a219-169">存取路徑</span><span class="sxs-lookup"><span data-stu-id="0a219-169">Access Paths</span></span> |<span data-ttu-id="0a219-170">[存取路徑]  資料行會顯示磁碟區的存取路徑。</span><span class="sxs-lookup"><span data-stu-id="0a219-170">The **Access Paths** column displays the access path to the volume.</span></span> <span data-ttu-id="0a219-171">這是可在主機電腦上存取磁碟區的磁碟機代號或掛接點。</span><span class="sxs-lookup"><span data-stu-id="0a219-171">This is the drive letter or mount point at which the volume is accessible on the host computer.</span></span> |

## <a name="delete-a-volume"></a><span data-ttu-id="0a219-172">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-172">Delete a volume</span></span>
<span data-ttu-id="0a219-173">請使用下列程序，從 StorSimple Snapshot Manager 中刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-173">Use the following procedure to delete a volume from StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="0a219-174">如果磁碟區是任何磁碟區群組的一部分，則無法刪除。</span><span class="sxs-lookup"><span data-stu-id="0a219-174">You cannot delete a volume if it is a part of any volume group.</span></span> <span data-ttu-id="0a219-175">(磁碟區若是磁碟區群組的成員，無法對其使用刪除選項。)您必須刪除整個磁碟區群組，才能刪除磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-175">(The delete option is not available for volumes that are members of a volume group.) You must delete the entire volume group to delete the volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="0a219-176">若要刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-176">To delete a volume</span></span>
1. <span data-ttu-id="0a219-177">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0a219-177">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="0a219-178">在 [範圍] 窗格中，按一下 [磁碟區] 節點。</span><span class="sxs-lookup"><span data-stu-id="0a219-178">In the **Scope** pane, click the **Volumes** node.</span></span> 
3. <span data-ttu-id="0a219-179">在 [結果]  窗格中，以滑鼠右鍵按一下您想要刪除的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-179">In the **Results** pane, right-click the volume that you want to delete.</span></span>
4. <span data-ttu-id="0a219-180">在功能表上，按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-180">On the menu, click **Delete**.</span></span> 
   
    ![刪除磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. <span data-ttu-id="0a219-182">[刪除磁碟區] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0a219-182">The **Delete Volume** dialog box appears.</span></span> <span data-ttu-id="0a219-183">在文字方塊中輸入 **Confirm**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0a219-183">Type **Confirm** in the text box, and then click **OK**.</span></span>
6. <span data-ttu-id="0a219-184">根據預設，StorSimple Snapshot Manager 會先備份磁碟區，再將其刪除。</span><span class="sxs-lookup"><span data-stu-id="0a219-184">By default, StorSimple Snapshot Manager backs up a volume before deleting it.</span></span> <span data-ttu-id="0a219-185">此預防措施可讓您在意外刪除時避免資料損失。</span><span class="sxs-lookup"><span data-stu-id="0a219-185">This precaution can protect you from data loss if the deletion was unintentional.</span></span> <span data-ttu-id="0a219-186">StorSimple Snapshot Manager 會在備份磁碟區時顯示 [自動快照]  進度訊息。</span><span class="sxs-lookup"><span data-stu-id="0a219-186">StorSimple Snapshot Manager displays an **Automatic Snapshot** progress message while it backs up the volume.</span></span> 
   
    ![自動快照訊息](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a><span data-ttu-id="0a219-188">重新掃描磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-188">Rescan volumes</span></span>
<span data-ttu-id="0a219-189">請使用下列程序，來重新掃描已連接至 StorSimple Snapshot Manager 的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-189">Use the following procedure to rescan the volumes connected to StorSimple Snapshot Manager.</span></span>

#### <a name="to-rescan-the-volumes"></a><span data-ttu-id="0a219-190">若要重新掃描磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-190">To rescan the volumes</span></span>
1. <span data-ttu-id="0a219-191">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0a219-191">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="0a219-192">在 [範圍] 窗格中，以滑鼠右鍵按一下 [磁碟區]，然後按一下 [重新掃描磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="0a219-192">In the **Scope** pane, right-click **Volumes**, and then click **Rescan volumes**.</span></span>
   
    ![重新掃描磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    <span data-ttu-id="0a219-194">此程序會同步處理磁碟區清單與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0a219-194">This procedure synchronizes the volume list with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="0a219-195">任何變更 (例如新增的磁碟區或已刪除的磁碟區) 將會反映在結果中。</span><span class="sxs-lookup"><span data-stu-id="0a219-195">Any changes, such as new volumes or deleted volumes, will be reflected in the results.</span></span>

## <a name="configure-and-back-up-a-basic-volume"></a><span data-ttu-id="0a219-196">設定和備份基本磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-196">Configure and back up a basic volume</span></span>
<span data-ttu-id="0a219-197">請使用下列程序，來設定基本磁碟區的備份，然後立即啟動備份，或建立一個原則進行排程的備份。</span><span class="sxs-lookup"><span data-stu-id="0a219-197">Use the following procedure to configure a backup of a basic volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0a219-198">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a219-198">Prerequisites</span></span>
<span data-ttu-id="0a219-199">開始之前：</span><span class="sxs-lookup"><span data-stu-id="0a219-199">Before you begin:</span></span>

* <span data-ttu-id="0a219-200">確定已正確設定 StorSimple 裝置和主機電腦。</span><span class="sxs-lookup"><span data-stu-id="0a219-200">Make sure that the StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="0a219-201">如需詳細資訊，請移至 [部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="0a219-201">For more information, go to [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="0a219-202">安裝和設定 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0a219-202">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="0a219-203">如需詳細資訊，請移至 [部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="0a219-203">For more information, go to [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>

#### <a name="to-configure-backup-of-a-basic-volume"></a><span data-ttu-id="0a219-204">若要設定基本磁碟區的備份</span><span class="sxs-lookup"><span data-stu-id="0a219-204">To configure backup of a basic volume</span></span>
1. <span data-ttu-id="0a219-205">在 StorSimple 裝置上建立基本磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-205">Create a basic volume on the StorSimple device.</span></span>
2. <span data-ttu-id="0a219-206">依 [掛接磁碟區](#mount-volumes)所述掛接、初始化和格式化磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-206">Mount, initialize, and format the volume as described in [Mount volumes](#mount-volumes).</span></span> 
3. <span data-ttu-id="0a219-207">按一下桌面上的 StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="0a219-207">Click the StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="0a219-208">StorSimple Snapshot Manager 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0a219-208">The StorSimple Snapshot Manager window appears.</span></span> 
4. <span data-ttu-id="0a219-209">在 [範圍] 窗格中，以滑鼠右鍵按一下 [磁碟區] 節點，然後選取 [重新掃描磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="0a219-209">In the **Scope** pane, right-click the **Volumes** node, and then select **Rescan volumes**.</span></span> <span data-ttu-id="0a219-210">掃描完成時，磁碟區清單應該會出現在 [結果]  窗格中。</span><span class="sxs-lookup"><span data-stu-id="0a219-210">When the scan is finished, a list of volumes should appear in the **Results** pane.</span></span> 
5. <span data-ttu-id="0a219-211">在 [結果] 窗格中，以滑鼠右鍵按一下磁碟區，然後選取 [建立磁碟區群組]。</span><span class="sxs-lookup"><span data-stu-id="0a219-211">In the **Results** pane, right-click the volume, and then select **Create Volume Group**.</span></span> 
   
    ![建立磁碟區群組](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. <span data-ttu-id="0a219-213">在 [建立磁碟區群組] 對話方塊中，輸入磁碟區群組的名稱，並為其指派磁碟區，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0a219-213">In the **Create Volume Group** dialog box, type a name for the volume group, assign volumes to it, and then click **OK**.</span></span>
7. <span data-ttu-id="0a219-214">在 [範圍] 窗格中，展開 [磁碟區群組] 節點。</span><span class="sxs-lookup"><span data-stu-id="0a219-214">In the **Scope** pane, expand the **Volume Groups** node.</span></span> <span data-ttu-id="0a219-215">新的磁碟區群組應該會出現在 [磁碟區群組]  節點之下。</span><span class="sxs-lookup"><span data-stu-id="0a219-215">The new volume group should appear under the **Volume Groups** node.</span></span> 
8. <span data-ttu-id="0a219-216">以滑鼠右鍵按一下磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="0a219-216">Right-click the volume group name.</span></span>
   
   * <span data-ttu-id="0a219-217">若要以互動方式 (依需求) 啟動備份作業，請按一下 [進行備份] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-217">To start an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="0a219-218">若要排程自動備份，請按一下 [建立備份原則] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-218">To schedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="0a219-219">在 [一般]  頁面上，從清單中選取磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="0a219-219">On the **General** page, select a volume group from the list.</span></span> <span data-ttu-id="0a219-220">在 [排程]  頁面上，輸入排程詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0a219-220">On the **Schedule** page, enter the schedule details.</span></span> <span data-ttu-id="0a219-221">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-221">When you are finished, click **OK**.</span></span> 
9. <span data-ttu-id="0a219-222">若要確認備份作業已啟動，請展開 [範圍] 窗格中的 [作業] 節點，然後按一下 [執行中] 節點。</span><span class="sxs-lookup"><span data-stu-id="0a219-222">To confirm that the backup job has started, expand the **Jobs** node in the **Scope** pane, and then click the **Running** node.</span></span> <span data-ttu-id="0a219-223">目前執行中的工作清單會出現在 [結果]  窗格中。</span><span class="sxs-lookup"><span data-stu-id="0a219-223">The list of currently running jobs appears in the **Results** pane.</span></span> 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a><span data-ttu-id="0a219-224">設定和備份動態鏡像磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-224">Configure and back up a dynamic mirrored volume</span></span>
<span data-ttu-id="0a219-225">請完成下列步驟來設定動態鏡像磁碟區的備份：</span><span class="sxs-lookup"><span data-stu-id="0a219-225">Complete the following steps to configure backup of a dynamic mirrored volume:</span></span>

* <span data-ttu-id="0a219-226">步驟 1：使用 [磁碟管理] 來建立動態鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-226">Step 1: Use Disk Management to create a dynamic mirrored volume.</span></span> 
* <span data-ttu-id="0a219-227">步驟 2：使用 StorSimple Snapshot Manager 來設定備份。</span><span class="sxs-lookup"><span data-stu-id="0a219-227">Step 2: Use StorSimple Snapshot Manager to configure backup.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0a219-228">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a219-228">Prerequisites</span></span>
<span data-ttu-id="0a219-229">開始之前：</span><span class="sxs-lookup"><span data-stu-id="0a219-229">Before you begin:</span></span>

* <span data-ttu-id="0a219-230">確定已正確設定 StorSimple 裝置和主機電腦。</span><span class="sxs-lookup"><span data-stu-id="0a219-230">Make sure that the StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="0a219-231">如需詳細資訊，請移至 [部署內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="0a219-231">For more information, go to [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="0a219-232">安裝和設定 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="0a219-232">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="0a219-233">如需詳細資訊，請移至 [部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="0a219-233">For more information, go to [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
* <span data-ttu-id="0a219-234">在 StorSimple 裝置上設定兩個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-234">Configure two volumes on the StorSimple device.</span></span> <span data-ttu-id="0a219-235">(在這些範例中，可用的磁碟區為 [磁碟 1] 和 [磁碟 2]。)</span><span class="sxs-lookup"><span data-stu-id="0a219-235">(In the examples, the available volumes are **Disk 1** and **Disk 2**.)</span></span> 

### <a name="step-1-use-disk-management-to-create-a-dynamic-mirrored-volume"></a><span data-ttu-id="0a219-236">步驟 1：使用 [磁碟管理] 來建立動態鏡像磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-236">Step 1: Use Disk Management to create a dynamic mirrored volume</span></span>
<span data-ttu-id="0a219-237">[磁碟管理] 是一種系統公用程式，用於管理硬碟及其包含的磁碟區或磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="0a219-237">Disk Management is a system utility for managing hard disks and the volumes or partitions that they contain.</span></span> <span data-ttu-id="0a219-238">如需 [磁碟管理] 的詳細資訊，請移至 Microsoft TechNet 網站上的 [磁碟管理](https://technet.microsoft.com/library/cc770943.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="0a219-238">For more information about Disk Management, go to [Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on the Microsoft TechNet website.</span></span>

#### <a name="to-create-a-dynamic-mirrored-volume"></a><span data-ttu-id="0a219-239">若要建立動態鏡像磁碟區</span><span class="sxs-lookup"><span data-stu-id="0a219-239">To create a dynamic mirrored volume</span></span>
1. <span data-ttu-id="0a219-240">請使用下列任一個選項來啟動 [磁碟管理]：</span><span class="sxs-lookup"><span data-stu-id="0a219-240">Use any of the following options to start Disk Management:</span></span> 
   
   * <span data-ttu-id="0a219-241">開啟 [執行] 方塊，輸入 **Diskmgmt.msc**，然後按下 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="0a219-241">Open the **Run** box, type **Diskmgmt.msc**, and press Enter.</span></span>
   * <span data-ttu-id="0a219-242">啟動 [伺服器管理員]，展開 [儲存體] 節點，然後選取 [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="0a219-242">Start Server Manager, expand the **Storage** node, and then select **Disk Management**.</span></span> 
   * <span data-ttu-id="0a219-243">啟動 [系統管理工具]，展開 [電腦管理] 節點，然後選取 [磁碟管理]。</span><span class="sxs-lookup"><span data-stu-id="0a219-243">Start **Administrative Tools**, expand the **Computer Management** node, and then select **Disk Management**.</span></span> 
2. <span data-ttu-id="0a219-244">確定您在 StorSimple 裝置上有兩個可用的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-244">Make sure that you have two volumes available on the StorSimple device.</span></span> <span data-ttu-id="0a219-245">(在此範例中，可用的磁碟區為 [磁碟 1] 和 [磁碟 2])。</span><span class="sxs-lookup"><span data-stu-id="0a219-245">(In the example, the available volumes are **Disk 1** and **Disk 2**.)</span></span> 
3. <span data-ttu-id="0a219-246">在 [磁碟管理] 視窗中，於下方窗格右邊的資料行中，以滑鼠右鍵按一下 [磁碟 1]，然後選取 [新增鏡像磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="0a219-246">In the Disk Management window, in the right column of the lower pane, right-click **Disk 1** and select **New Mirrored Volume**.</span></span> 
   
    ![新鏡像磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. <span data-ttu-id="0a219-248">在 [新增鏡像磁碟區] 精靈頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a219-248">On the **New Mirrored Volume** wizard page, click **Next**.</span></span>
5. <span data-ttu-id="0a219-249">在 [選取磁碟] 頁面上，於 [已選取] 窗格中選取 [磁碟 2]，按一下 [新增]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a219-249">On the **Select Disks** page, select **Disk 2** in the **Selected** pane, click **Add**, and then click **Next**.</span></span> 
6. <span data-ttu-id="0a219-250">在 [指派磁碟機代號或路徑] 頁面上，接受預設值，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a219-250">On the **Assign Drive Letter or Path** page, accept the defaults, and then click **Next**.</span></span> 
7. <span data-ttu-id="0a219-251">在 [格式化磁碟區] 頁面上，於 [配置單位大小] 方塊中，選取 [64K]。</span><span class="sxs-lookup"><span data-stu-id="0a219-251">On the **Format Volume** page, in the **Allocation Unit Size** box, select **64K**.</span></span> <span data-ttu-id="0a219-252">選取 [執行快速格式化] 核取方塊，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="0a219-252">Select the **Perform a quick format** check box, and then click **Next**.</span></span> 
8. <span data-ttu-id="0a219-253">在 [完成新增鏡像磁碟區] 頁面上，檢閱您的設定，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="0a219-253">On the **Completing the New Mirrored Volume** page, review your settings, and then click **Finish**.</span></span> 
9. <span data-ttu-id="0a219-254">訊息會出現，以指出基本磁碟將會轉換成動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="0a219-254">A message appears to indicate that the basic disk will be converted to a dynamic disk.</span></span> <span data-ttu-id="0a219-255">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-255">Click **Yes**.</span></span>
   
    ![動態磁碟轉換訊息](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. <span data-ttu-id="0a219-257">在磁碟管理中，確認磁碟區 1 與磁碟區 2 顯示為動態鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-257">In Disk Management, verify that Disk 1 and Disk 2 are shown as dynamic mirrored volumes.</span></span> <span data-ttu-id="0a219-258">(狀態欄中應該會顯示 [動態]，容量條顏色應變為紅色表示鏡像磁碟區。)</span><span class="sxs-lookup"><span data-stu-id="0a219-258">(**Dynamic** should appear in the status column, and the capacity bar color should change to red, indicating a mirrored volume.)</span></span> 
    
    ![磁碟管理的鏡像動態磁碟](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-to-configure-backup"></a><span data-ttu-id="0a219-260">步驟 2：使用 StorSimple Snapshot Manager 來設定備份</span><span class="sxs-lookup"><span data-stu-id="0a219-260">Step 2: Use StorSimple Snapshot Manager to configure backup</span></span>
<span data-ttu-id="0a219-261">請使用下列程序，來設定動態鏡像磁碟區，然後立即啟動備份，或建立一個原則進行排程的備份。</span><span class="sxs-lookup"><span data-stu-id="0a219-261">Use the following procedure to configure a dynamic mirrored volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

#### <a name="to-configure-backup-of-a-dynamic-mirrored-volume"></a><span data-ttu-id="0a219-262">若要設定動態鏡像磁碟區的備份</span><span class="sxs-lookup"><span data-stu-id="0a219-262">To configure backup of a dynamic mirrored volume</span></span>
1. <span data-ttu-id="0a219-263">按一下桌面上的 StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="0a219-263">Click the StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="0a219-264">StorSimple Snapshot Manager 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0a219-264">The StorSimple Snapshot Manager window appears.</span></span> 
2. <span data-ttu-id="0a219-265">在 [範圍] 窗格中，以滑鼠右鍵按一下 [磁碟區] 節點，然後選取 [重新掃描磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="0a219-265">In the **Scope** pane, right-click the **Volumes** node and select **Rescan volumes**.</span></span> <span data-ttu-id="0a219-266">掃描完成時，磁碟區清單應該會出現在 [結果]  窗格中。</span><span class="sxs-lookup"><span data-stu-id="0a219-266">When the scan is finished, a list of volumes should appear in the **Results** pane.</span></span> <span data-ttu-id="0a219-267">動態鏡像磁碟區會列為單一磁碟區。</span><span class="sxs-lookup"><span data-stu-id="0a219-267">The dynamic mirrored volume is listed as a single volume.</span></span> 
3. <span data-ttu-id="0a219-268">在 [結果] 窗格中，以滑鼠右鍵按一下動態鏡像磁碟區，然後按一下 [建立磁碟區群組]。</span><span class="sxs-lookup"><span data-stu-id="0a219-268">In the **Results** pane, right-click the dynamic mirrored volume, and then click **Create Volume Group**.</span></span> 
4. <span data-ttu-id="0a219-269">在 [建立磁碟區群組] 對話方塊中，輸入磁碟區群組的名稱，將動態鏡像磁碟區指派給這個群組，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0a219-269">In the **Create Volume Group** dialog box, type a name for the volume group, assign the dynamic mirrored volume to this group, and then click **OK**.</span></span> 
5. <span data-ttu-id="0a219-270">在 [範圍] 窗格中，展開 [磁碟區群組] 節點。</span><span class="sxs-lookup"><span data-stu-id="0a219-270">In the **Scope** pane, expand the **Volume Groups** node.</span></span> <span data-ttu-id="0a219-271">新的磁碟區群組應該會出現在 [磁碟區群組] 節點之下。</span><span class="sxs-lookup"><span data-stu-id="0a219-271">The new volume group should appear under the  **Volume Groups** node.</span></span> 
6. <span data-ttu-id="0a219-272">以滑鼠右鍵按一下磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="0a219-272">Right-click the volume group name.</span></span> 
   
   * <span data-ttu-id="0a219-273">若要以互動方式 (依需求) 啟動備份作業，請按一下 [進行備份] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-273">To start an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="0a219-274">若要排程自動備份，請按一下 [建立備份原則] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-274">To schedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="0a219-275">在 [一般]  頁面上，從清單中選取該磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="0a219-275">On the **General** page, select the volume group from the list.</span></span> <span data-ttu-id="0a219-276">在 [排程]  頁面上，輸入排程詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0a219-276">On the **Schedule** page, enter the schedule details.</span></span> <span data-ttu-id="0a219-277">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0a219-277">When you are finished, click **OK**.</span></span> 
7. <span data-ttu-id="0a219-278">您可以在備份作業執行時加以監視。</span><span class="sxs-lookup"><span data-stu-id="0a219-278">You can monitor the backup job as it runs.</span></span> <span data-ttu-id="0a219-279">在 [範圍] 窗格中，展開 [作業] 節點，然後按一下 [執行中]。作業詳細資料會出現在 [結果] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="0a219-279">In the **Scope** pane, expand the **Jobs** node, and then click **Running**, The job details appear in the **Results** pane.</span></span> <span data-ttu-id="0a219-280">備份作業完成時，詳細資料會傳輸至 [過去 24 小時] 作業清單。</span><span class="sxs-lookup"><span data-stu-id="0a219-280">When the backup job is finished, the details are transferred to the **Last 24** hours job list.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0a219-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a219-281">Next steps</span></span>
* <span data-ttu-id="0a219-282">了解如何 [使用 StorSimple Snapshot Manager 來管理您的 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="0a219-282">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="0a219-283">了解如何 [使用 StorSimple Snapshot Manager 來建立和管理磁碟區群組](storsimple-snapshot-manager-manage-volume-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="0a219-283">Learn how to [use StorSimple Snapshot Manager to create and manage volume groups](storsimple-snapshot-manager-manage-volume-groups.md).</span></span>

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
