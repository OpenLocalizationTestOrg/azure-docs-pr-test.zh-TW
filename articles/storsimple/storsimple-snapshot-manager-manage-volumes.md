---
title: "aaaStorSimple Snapshot Manager 和磁碟區 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooview 和管理磁碟區和 tooconfigure 備份。"
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
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a><span data-ttu-id="25984-103">使用 StorSimple Snapshot Manager tooview 及管理磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-103">Use StorSimple Snapshot Manager tooview and manage volumes</span></span>
## <a name="overview"></a><span data-ttu-id="25984-104">概觀</span><span class="sxs-lookup"><span data-stu-id="25984-104">Overview</span></span>
<span data-ttu-id="25984-105">您可以使用 hello StorSimple Snapshot Manager**磁碟區**節點 (在 hello**範圍**窗格) tooselect 磁碟區，並檢視其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="25984-105">You can use hello StorSimple Snapshot Manager **Volumes** node (on hello **Scope** pane) tooselect volumes and view information about them.</span></span> <span data-ttu-id="25984-106">hello 磁碟區會顯示為對應 toohello hello 主機所掛接的磁碟區的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="25984-106">hello volumes are presented as drives that correspond toohello volumes mounted by hello host.</span></span> <span data-ttu-id="25984-107">hello**磁碟區**節點會顯示本機磁碟區和支援的 StorSimple，包括透過 iSCSI 及裝置 hello 使用探索到的磁碟區的磁碟區類型。</span><span class="sxs-lookup"><span data-stu-id="25984-107">hello **Volumes** node shows local volumes and volume types that are supported by StorSimple, including volumes discovered through hello use of iSCSI and a device.</span></span> 

<span data-ttu-id="25984-108">如需有關支援的磁碟區的詳細資訊，請移至太[支援多個磁碟區類型](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types)。</span><span class="sxs-lookup"><span data-stu-id="25984-108">For more information about supported volumes, go too[Support for multiple volume types](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).</span></span>

![在 [結果] 窗格中的磁碟區清單](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

<span data-ttu-id="25984-110">hello**磁碟區**節點也可讓您重新掃描或刪除磁碟區之後 StorSimple Snapshot Manager 探索它們。</span><span class="sxs-lookup"><span data-stu-id="25984-110">hello **Volumes** node also lets you rescan or delete volumes after StorSimple Snapshot Manager discovers them.</span></span> 

<span data-ttu-id="25984-111">本教學課程說明如何掛載、初始化和格式化磁碟區，然後使用 StorSimple Snapshot Manager：</span><span class="sxs-lookup"><span data-stu-id="25984-111">This tutorial explains how you can mount, initialize, and format volumes and then use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="25984-112">檢視磁碟區的相關資訊</span><span class="sxs-lookup"><span data-stu-id="25984-112">View information about volumes</span></span> 
* <span data-ttu-id="25984-113">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-113">Delete volumes</span></span>
* <span data-ttu-id="25984-114">重新掃描磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-114">Rescan volumes</span></span> 
* <span data-ttu-id="25984-115">設定基本磁碟區並將其備份</span><span class="sxs-lookup"><span data-stu-id="25984-115">Configure a basic volume and back it up</span></span>
* <span data-ttu-id="25984-116">設定動態鏡像磁碟區並將其備份</span><span class="sxs-lookup"><span data-stu-id="25984-116">Configure a dynamic mirrored volume and back it up</span></span>

> [!NOTE]
> <span data-ttu-id="25984-117">所有 hello**磁碟區**節點動作也會提供在 hello**動作**窗格。</span><span class="sxs-lookup"><span data-stu-id="25984-117">All of hello **Volume** node actions are also available in hello **Actions** pane.</span></span>
> 
> 

## <a name="mount-volumes"></a><span data-ttu-id="25984-118">掛接磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-118">Mount volumes</span></span>
<span data-ttu-id="25984-119">使用 hello 下列程序 toomount 初始化及格式化 StorSimple 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-119">Use hello following procedure toomount, initialize, and format StorSimple volumes.</span></span> <span data-ttu-id="25984-120">此程序會使用磁碟管理 中的系統公用程式管理硬碟與 hello 對應的磁碟區或磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="25984-120">This procedure uses Disk Management, a system utility for managing hard disks and hello corresponding volumes or partitions.</span></span> <span data-ttu-id="25984-121">如需磁碟管理的詳細資訊，請移過[磁碟管理](https://technet.microsoft.com/library/cc770943.aspx)hello Microsoft TechNet 網站上。</span><span class="sxs-lookup"><span data-stu-id="25984-121">For more information about Disk Management, go too[Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on hello Microsoft TechNet website.</span></span>

#### <a name="toomount-volumes"></a><span data-ttu-id="25984-122">toomount 磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-122">toomount volumes</span></span>
1. <span data-ttu-id="25984-123">在您的主機電腦上啟動 hello Microsoft iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="25984-123">On your host computer, start hello Microsoft iSCSI initiator.</span></span>
2. <span data-ttu-id="25984-124">提供一個 hello 介面 IP 位址為 「 hello 目標入口網站或探索 IP 位址，然後再 toohello 裝置連線。</span><span class="sxs-lookup"><span data-stu-id="25984-124">Supply one of hello interface IP addresses as hello target portal or discovery IP address, and connect toohello device.</span></span> <span data-ttu-id="25984-125">Hello 裝置連線之後，hello 磁碟區會存取 tooyour Windows 系統。</span><span class="sxs-lookup"><span data-stu-id="25984-125">After hello device is connected, hello volumes will be accessible tooyour Windows system.</span></span> <span data-ttu-id="25984-126">如需有關使用 hello Microsoft iSCSI 啟動器的詳細資訊，請進入 toohello > 一節 「 連接 tooan iSCSI 目標裝置 」[安裝和設定 Microsoft iSCSI 啟動器][1]。</span><span class="sxs-lookup"><span data-stu-id="25984-126">For more information about using hello Microsoft iSCSI initiator, go toohello section “Connecting tooan iSCSI target device” in [Installing and Configuring Microsoft iSCSI Initiator][1].</span></span>
3. <span data-ttu-id="25984-127">使用任何下列選項 toostart 磁碟管理的 hello:</span><span class="sxs-lookup"><span data-stu-id="25984-127">Use any of hello following options toostart Disk Management:</span></span>
   
   * <span data-ttu-id="25984-128">輸入 hello Diskmgmt.msc**執行**方塊。</span><span class="sxs-lookup"><span data-stu-id="25984-128">Type Diskmgmt.msc in hello **Run** box.</span></span>
   * <span data-ttu-id="25984-129">啟動 伺服器管理員中，展開 hello**儲存體**節點，然後再選取**磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="25984-129">Start Server Manager, expand hello **Storage** node, and then select **Disk Management**.</span></span>
   * <span data-ttu-id="25984-130">啟動**系統管理工具**，依序展開 hello**電腦管理**節點，然後再選取**磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="25984-130">Start **Administrative Tools**, expand hello **Computer Management** node, and then select **Disk Management**.</span></span> 
     
     > [!NOTE]
     > <span data-ttu-id="25984-131">您必須使用系統管理員權限 toorun 磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="25984-131">You must use administrator privileges toorun Disk Management.</span></span>
     > 
     > 
4. <span data-ttu-id="25984-132">線上採取 hello 的磁碟區：</span><span class="sxs-lookup"><span data-stu-id="25984-132">Take hello volume(s) online:</span></span>
   
   1. <span data-ttu-id="25984-133">在 [磁碟管理] 中，以滑鼠右鍵按一下任何標示為 [離線] 的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-133">In Disk Management, right-click any volume marked **Offline**.</span></span>
   2. <span data-ttu-id="25984-134">按一下 [重新啟動磁碟] 。</span><span class="sxs-lookup"><span data-stu-id="25984-134">Click **Reactivate Disk**.</span></span> <span data-ttu-id="25984-135">hello 磁碟應標示為**線上**hello 磁碟重新啟動之後。</span><span class="sxs-lookup"><span data-stu-id="25984-135">hello disk should be marked **Online** after hello disk is reactivated.</span></span>
5. <span data-ttu-id="25984-136">初始化 hello 的磁碟區：</span><span class="sxs-lookup"><span data-stu-id="25984-136">Initialize hello volume(s):</span></span>
   
   1. <span data-ttu-id="25984-137">以滑鼠右鍵按一下探索到的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-137">Right-click hello discovered volumes.</span></span>
   2. <span data-ttu-id="25984-138">在 hello 功能表中，選取 **初始化磁碟**。</span><span class="sxs-lookup"><span data-stu-id="25984-138">On hello menu, select **Initialize Disk**.</span></span>
   3. <span data-ttu-id="25984-139">在 hello**初始化磁碟**對話方塊中，您想 tooinitialize，然後再按一下選取的 hello 磁碟**確定**。</span><span class="sxs-lookup"><span data-stu-id="25984-139">In hello **Initialize Disk** dialog box, select hello disks that you want tooinitialize, and then click **OK**.</span></span>
6. <span data-ttu-id="25984-140">格式化簡單磁碟區：</span><span class="sxs-lookup"><span data-stu-id="25984-140">Format simple volumes:</span></span>
   
   1. <span data-ttu-id="25984-141">以滑鼠右鍵按一下您想 tooformat 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-141">Right-click a volume that you want tooformat.</span></span>
   2. <span data-ttu-id="25984-142">在 hello 功能表中，選取 **新增簡單磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="25984-142">On hello menu, select **New Simple Volume**.</span></span>
   3. <span data-ttu-id="25984-143">使用 hello 新增簡單磁碟區精靈 tooformat hello 磁碟區：</span><span class="sxs-lookup"><span data-stu-id="25984-143">Use hello New Simple Volume wizard tooformat hello volume:</span></span>
      
      * <span data-ttu-id="25984-144">指定 hello 磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="25984-144">Specify hello volume size.</span></span>
      * <span data-ttu-id="25984-145">提供磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="25984-145">Supply a drive letter.</span></span>
      * <span data-ttu-id="25984-146">選取 hello NTFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="25984-146">Select hello NTFS file system.</span></span>
      * <span data-ttu-id="25984-147">指定 64 KB 的配置單位大小。</span><span class="sxs-lookup"><span data-stu-id="25984-147">Specify a 64 KB allocation unit size.</span></span>
      * <span data-ttu-id="25984-148">執行快速格式化。</span><span class="sxs-lookup"><span data-stu-id="25984-148">Perform a quick format.</span></span>
7. <span data-ttu-id="25984-149">格式化多重磁碟分割磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-149">Format multi-partition volumes.</span></span> <span data-ttu-id="25984-150">如需指示，請移 toohello 區段中，「 磁碟分割與磁碟區 」[實作磁碟管理](https://msdn.microsoft.com/library/dd163556.aspx)。</span><span class="sxs-lookup"><span data-stu-id="25984-150">For instructions, go toohello section, "Partitions and Volumes" in [Implementing Disk Management](https://msdn.microsoft.com/library/dd163556.aspx).</span></span>

## <a name="view-information-about-your-volumes"></a><span data-ttu-id="25984-151">檢視您磁碟區的相關資訊</span><span class="sxs-lookup"><span data-stu-id="25984-151">View information about your volumes</span></span>
<span data-ttu-id="25984-152">使用下列程序 tooview 資訊有關本機和 Azure StorSimple 磁碟區的 hello。</span><span class="sxs-lookup"><span data-stu-id="25984-152">Use hello following procedure tooview information about local and Azure StorSimple volumes.</span></span>

#### <a name="tooview-volume-information"></a><span data-ttu-id="25984-153">tooview 磁碟區資訊</span><span class="sxs-lookup"><span data-stu-id="25984-153">tooview volume information</span></span>
1. <span data-ttu-id="25984-154">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="25984-154">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="25984-155">在 [hello**範圍**] 窗格中，按一下 hello**磁碟區**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-155">In hello **Scope** pane, click hello **Volumes** node.</span></span> <span data-ttu-id="25984-156">本機與掛接磁碟區，包括所有 Azure StorSimple 磁碟區，清單會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="25984-156">A list of local and mounted volumes, including all Azure StorSimple volumes, appears in hello **Results** pane.</span></span> <span data-ttu-id="25984-157">hello hello 中的資料行**結果**窗格可加以設定。</span><span class="sxs-lookup"><span data-stu-id="25984-157">hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="25984-158">(以滑鼠右鍵按一下 hello**磁碟區**節點中，選取**檢視**，然後選取**新增/移除欄位**。)</span><span class="sxs-lookup"><span data-stu-id="25984-158">(Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>
   
    ![設定 hello 資料行](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | <span data-ttu-id="25984-160">結果資料行</span><span class="sxs-lookup"><span data-stu-id="25984-160">Results column</span></span> | <span data-ttu-id="25984-161">說明</span><span class="sxs-lookup"><span data-stu-id="25984-161">Description</span></span> |
   |:--- |:--- |
   |  <span data-ttu-id="25984-162">名稱</span><span class="sxs-lookup"><span data-stu-id="25984-162">Name</span></span> |<span data-ttu-id="25984-163">hello**名稱**資料行包含 hello 磁碟機代號指派 tooeach 探索到的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-163">hello **Name** column contains hello drive letter assigned tooeach discovered volume.</span></span> |
   |  <span data-ttu-id="25984-164">裝置</span><span class="sxs-lookup"><span data-stu-id="25984-164">Device</span></span> |<span data-ttu-id="25984-165">hello**裝置**資料行包含 hello hello 裝置連線的 toohello 主機電腦的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="25984-165">hello **Device** column contains hello IP address of hello device connected toohello host computer.</span></span> |
   |  <span data-ttu-id="25984-166">裝置磁碟區名稱</span><span class="sxs-lookup"><span data-stu-id="25984-166">Device Volume Name</span></span> |<span data-ttu-id="25984-167">hello**裝置磁碟區名稱**資料行包含 hello 名稱 hello 裝置磁碟區 toowhich hello 選取磁碟區所屬。</span><span class="sxs-lookup"><span data-stu-id="25984-167">hello **Device Volume Name** column contains hello name of hello device volume toowhich hello selected volume belongs.</span></span> <span data-ttu-id="25984-168">這是定義在 hello 該特定磁碟區的 Azure 入口網站中的 hello 磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="25984-168">This is hello volume name defined in hello Azure portal for that specific volume.</span></span> |
   |  <span data-ttu-id="25984-169">存取路徑</span><span class="sxs-lookup"><span data-stu-id="25984-169">Access Paths</span></span> |<span data-ttu-id="25984-170">hello**存取路徑**資料行會顯示 hello 存取路徑 toohello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-170">hello **Access Paths** column displays hello access path toohello volume.</span></span> <span data-ttu-id="25984-171">這是 hello 存取磁碟機代號或掛接點的 hello 在磁碟區 hello 主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="25984-171">This is hello drive letter or mount point at which hello volume is accessible on hello host computer.</span></span> |

## <a name="delete-a-volume"></a><span data-ttu-id="25984-172">刪除磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-172">Delete a volume</span></span>
<span data-ttu-id="25984-173">使用下列程序 toodelete 磁碟區從 StorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="25984-173">Use hello following procedure toodelete a volume from StorSimple Snapshot Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="25984-174">如果磁碟區是任何磁碟區群組的一部分，則無法刪除。</span><span class="sxs-lookup"><span data-stu-id="25984-174">You cannot delete a volume if it is a part of any volume group.</span></span> <span data-ttu-id="25984-175">（hello 刪除選項不適用於磁碟區的磁碟區群組的成員。）您必須刪除 hello 整個磁碟區群組 toodelete hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-175">(hello delete option is not available for volumes that are members of a volume group.) You must delete hello entire volume group toodelete hello volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="25984-176">toodelete 磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-176">toodelete a volume</span></span>
1. <span data-ttu-id="25984-177">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="25984-177">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="25984-178">在 [hello**範圍**] 窗格中，按一下 hello**磁碟區**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-178">In hello **Scope** pane, click hello **Volumes** node.</span></span> 
3. <span data-ttu-id="25984-179">在 hello**結果**窗格中，以滑鼠右鍵按一下您想 toodelete 的 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-179">In hello **Results** pane, right-click hello volume that you want toodelete.</span></span>
4. <span data-ttu-id="25984-180">在 [hello] 功能表上按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="25984-180">On hello menu, click **Delete**.</span></span> 
   
    ![刪除磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. <span data-ttu-id="25984-182">hello**刪除磁碟區** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="25984-182">hello **Delete Volume** dialog box appears.</span></span> <span data-ttu-id="25984-183">型別**確認**在 hello 文字方塊中，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="25984-183">Type **Confirm** in hello text box, and then click **OK**.</span></span>
6. <span data-ttu-id="25984-184">根據預設，StorSimple Snapshot Manager 會先備份磁碟區，再將其刪除。</span><span class="sxs-lookup"><span data-stu-id="25984-184">By default, StorSimple Snapshot Manager backs up a volume before deleting it.</span></span> <span data-ttu-id="25984-185">此預防措施可以保護您免於資料遺失如果 hello 刪除是無意。</span><span class="sxs-lookup"><span data-stu-id="25984-185">This precaution can protect you from data loss if hello deletion was unintentional.</span></span> <span data-ttu-id="25984-186">StorSimple Snapshot Manager 顯示**自動快照**hello 磁碟區備份時的進度訊息。</span><span class="sxs-lookup"><span data-stu-id="25984-186">StorSimple Snapshot Manager displays an **Automatic Snapshot** progress message while it backs up hello volume.</span></span> 
   
    ![自動快照訊息](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a><span data-ttu-id="25984-188">重新掃描磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-188">Rescan volumes</span></span>
<span data-ttu-id="25984-189">使用下列程序 toorescan hello 磁碟區連接的 tooStorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="25984-189">Use hello following procedure toorescan hello volumes connected tooStorSimple Snapshot Manager.</span></span>

#### <a name="toorescan-hello-volumes"></a><span data-ttu-id="25984-190">toorescan hello 磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-190">toorescan hello volumes</span></span>
1. <span data-ttu-id="25984-191">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="25984-191">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="25984-192">在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**磁碟區**，然後按一下**重新掃描磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="25984-192">In hello **Scope** pane, right-click **Volumes**, and then click **Rescan volumes**.</span></span>
   
    ![重新掃描磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    <span data-ttu-id="25984-194">此程序同步處理 hello 磁碟區清單與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="25984-194">This procedure synchronizes hello volume list with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="25984-195">例如新的磁碟區或已刪除的磁碟區的任何變更將反映在 hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="25984-195">Any changes, such as new volumes or deleted volumes, will be reflected in hello results.</span></span>

## <a name="configure-and-back-up-a-basic-volume"></a><span data-ttu-id="25984-196">設定和備份基本磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-196">Configure and back up a basic volume</span></span>
<span data-ttu-id="25984-197">使用下列程序 tooconfigure 的基本磁碟區，備份的 hello 然後立即啟動備份，或建立排定的備份原則。</span><span class="sxs-lookup"><span data-stu-id="25984-197">Use hello following procedure tooconfigure a backup of a basic volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="25984-198">必要條件</span><span class="sxs-lookup"><span data-stu-id="25984-198">Prerequisites</span></span>
<span data-ttu-id="25984-199">開始之前：</span><span class="sxs-lookup"><span data-stu-id="25984-199">Before you begin:</span></span>

* <span data-ttu-id="25984-200">請確定已正確設定 hello StorSimple 裝置與主機電腦。</span><span class="sxs-lookup"><span data-stu-id="25984-200">Make sure that hello StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="25984-201">如需詳細資訊，請移至太[部署在內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="25984-201">For more information, go too[Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="25984-202">安裝和設定 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="25984-202">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="25984-203">如需詳細資訊，請移至太[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="25984-203">For more information, go too[Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>

#### <a name="tooconfigure-backup-of-a-basic-volume"></a><span data-ttu-id="25984-204">tooconfigure 的基本磁碟區備份</span><span class="sxs-lookup"><span data-stu-id="25984-204">tooconfigure backup of a basic volume</span></span>
1. <span data-ttu-id="25984-205">Hello StorSimple 裝置上建立基本磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-205">Create a basic volume on hello StorSimple device.</span></span>
2. <span data-ttu-id="25984-206">掛接、 初始化及格式化 hello 磁碟區中所述[掛接磁碟區](#mount-volumes)。</span><span class="sxs-lookup"><span data-stu-id="25984-206">Mount, initialize, and format hello volume as described in [Mount volumes](#mount-volumes).</span></span> 
3. <span data-ttu-id="25984-207">按一下桌面上的 hello StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="25984-207">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="25984-208">hello StorSimple Snapshot Manager 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="25984-208">hello StorSimple Snapshot Manager window appears.</span></span> 
4. <span data-ttu-id="25984-209">在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**磁碟區**節點，然後再選取**重新掃描磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="25984-209">In hello **Scope** pane, right-click hello **Volumes** node, and then select **Rescan volumes**.</span></span> <span data-ttu-id="25984-210">Hello 掃描完成時，磁碟區清單應該會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="25984-210">When hello scan is finished, a list of volumes should appear in hello **Results** pane.</span></span> 
5. <span data-ttu-id="25984-211">在 [hello**結果**] 窗格中，hello 磁碟區，以滑鼠右鍵按一下，然後選取**建立磁碟區群組**。</span><span class="sxs-lookup"><span data-stu-id="25984-211">In hello **Results** pane, right-click hello volume, and then select **Create Volume Group**.</span></span> 
   
    ![建立磁碟區群組](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. <span data-ttu-id="25984-213">在 hello**建立磁碟區群組**對話方塊中，輸入 hello 磁碟區群組的名稱，指定磁碟區 tooit，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="25984-213">In hello **Create Volume Group** dialog box, type a name for hello volume group, assign volumes tooit, and then click **OK**.</span></span>
7. <span data-ttu-id="25984-214">在 [hello**範圍**] 窗格中，展開 hello**磁碟區群組**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-214">In hello **Scope** pane, expand hello **Volume Groups** node.</span></span> <span data-ttu-id="25984-215">hello 新磁碟區群組應該會出現在 hello**磁碟區群組**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-215">hello new volume group should appear under hello **Volume Groups** node.</span></span> 
8. <span data-ttu-id="25984-216">以滑鼠右鍵按一下 hello 磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="25984-216">Right-click hello volume group name.</span></span>
   
   * <span data-ttu-id="25984-217">按一下 toostart 互動式 （隨） 備份工作，**取得備份**。</span><span class="sxs-lookup"><span data-stu-id="25984-217">toostart an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="25984-218">tooschedule 的自動備份中，按一下**建立備份原則**。</span><span class="sxs-lookup"><span data-stu-id="25984-218">tooschedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="25984-219">在 hello**一般**頁面上，從 hello 清單中選取磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="25984-219">On hello **General** page, select a volume group from hello list.</span></span> <span data-ttu-id="25984-220">在 hello**排程**頁面上，輸入 hello 排程詳細資料。</span><span class="sxs-lookup"><span data-stu-id="25984-220">On hello **Schedule** page, enter hello schedule details.</span></span> <span data-ttu-id="25984-221">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="25984-221">When you are finished, click **OK**.</span></span> 
9. <span data-ttu-id="25984-222">hello 備份作業的 tooconfirm 已啟動，展開 [hello**作業**節點 hello**範圍**] 窗格中，然後按一下hello**執行**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-222">tooconfirm that hello backup job has started, expand hello **Jobs** node in hello **Scope** pane, and then click hello **Running** node.</span></span> <span data-ttu-id="25984-223">hello 清單目前執行的工作會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="25984-223">hello list of currently running jobs appears in hello **Results** pane.</span></span> 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a><span data-ttu-id="25984-224">設定和備份動態鏡像磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-224">Configure and back up a dynamic mirrored volume</span></span>
<span data-ttu-id="25984-225">完成下列步驟 tooconfigure 備份動態鏡像磁碟區的 hello:</span><span class="sxs-lookup"><span data-stu-id="25984-225">Complete hello following steps tooconfigure backup of a dynamic mirrored volume:</span></span>

* <span data-ttu-id="25984-226">步驟 1： 使用 磁碟管理 toocreate 動態鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-226">Step 1: Use Disk Management toocreate a dynamic mirrored volume.</span></span> 
* <span data-ttu-id="25984-227">步驟 2： 使用 StorSimple Snapshot Manager tooconfigure 備份。</span><span class="sxs-lookup"><span data-stu-id="25984-227">Step 2: Use StorSimple Snapshot Manager tooconfigure backup.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="25984-228">必要條件</span><span class="sxs-lookup"><span data-stu-id="25984-228">Prerequisites</span></span>
<span data-ttu-id="25984-229">開始之前：</span><span class="sxs-lookup"><span data-stu-id="25984-229">Before you begin:</span></span>

* <span data-ttu-id="25984-230">請確定已正確設定 hello StorSimple 裝置與主機電腦。</span><span class="sxs-lookup"><span data-stu-id="25984-230">Make sure that hello StorSimple device and host computer are configured correctly.</span></span> <span data-ttu-id="25984-231">如需詳細資訊，請移至太[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="25984-231">For more information, go too[Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>
* <span data-ttu-id="25984-232">安裝和設定 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="25984-232">Install and configure StorSimple Snapshot Manager.</span></span> <span data-ttu-id="25984-233">如需詳細資訊，請移至太[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="25984-233">For more information, go too[Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
* <span data-ttu-id="25984-234">Hello StorSimple 裝置上設定兩個磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-234">Configure two volumes on hello StorSimple device.</span></span> <span data-ttu-id="25984-235">(在 hello 範例與 hello 可用的磁碟區為**磁碟 1**和**磁碟 2**。)</span><span class="sxs-lookup"><span data-stu-id="25984-235">(In hello examples, hello available volumes are **Disk 1** and **Disk 2**.)</span></span> 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a><span data-ttu-id="25984-236">步驟 1： 使用 磁碟管理 toocreate 動態鏡像磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-236">Step 1: Use Disk Management toocreate a dynamic mirrored volume</span></span>
<span data-ttu-id="25984-237">磁碟管理 是管理硬碟與 hello 磁碟區或其所包含的資料分割的系統公用程式。</span><span class="sxs-lookup"><span data-stu-id="25984-237">Disk Management is a system utility for managing hard disks and hello volumes or partitions that they contain.</span></span> <span data-ttu-id="25984-238">如需磁碟管理的詳細資訊，請移過[磁碟管理](https://technet.microsoft.com/library/cc770943.aspx)hello Microsoft TechNet 網站上。</span><span class="sxs-lookup"><span data-stu-id="25984-238">For more information about Disk Management, go too[Disk Management](https://technet.microsoft.com/library/cc770943.aspx) on hello Microsoft TechNet website.</span></span>

#### <a name="toocreate-a-dynamic-mirrored-volume"></a><span data-ttu-id="25984-239">toocreate 動態鏡像磁碟區</span><span class="sxs-lookup"><span data-stu-id="25984-239">toocreate a dynamic mirrored volume</span></span>
1. <span data-ttu-id="25984-240">使用任何下列選項 toostart 磁碟管理的 hello:</span><span class="sxs-lookup"><span data-stu-id="25984-240">Use any of hello following options toostart Disk Management:</span></span> 
   
   * <span data-ttu-id="25984-241">開啟 hello**執行**方塊中，輸入**Diskmgmt.msc**，然後按 Enter。</span><span class="sxs-lookup"><span data-stu-id="25984-241">Open hello **Run** box, type **Diskmgmt.msc**, and press Enter.</span></span>
   * <span data-ttu-id="25984-242">啟動 伺服器管理員中，展開 hello**儲存體**節點，然後再選取**磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="25984-242">Start Server Manager, expand hello **Storage** node, and then select **Disk Management**.</span></span> 
   * <span data-ttu-id="25984-243">啟動**系統管理工具**，依序展開 hello**電腦管理**節點，然後再選取**磁碟管理**。</span><span class="sxs-lookup"><span data-stu-id="25984-243">Start **Administrative Tools**, expand hello **Computer Management** node, and then select **Disk Management**.</span></span> 
2. <span data-ttu-id="25984-244">請確定您有兩個可用的磁碟區 hello StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="25984-244">Make sure that you have two volumes available on hello StorSimple device.</span></span> <span data-ttu-id="25984-245">(在 hello 範例與 hello 可用的磁碟區為**磁碟 1**和**磁碟 2**。)</span><span class="sxs-lookup"><span data-stu-id="25984-245">(In hello example, hello available volumes are **Disk 1** and **Disk 2**.)</span></span> 
3. <span data-ttu-id="25984-246">在 hello 磁碟管理 視窗，hello 右邊資料行中的 hello 下方窗格中，以滑鼠右鍵按一下**磁碟 1**選取**新增鏡像磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="25984-246">In hello Disk Management window, in hello right column of hello lower pane, right-click **Disk 1** and select **New Mirrored Volume**.</span></span> 
   
    ![新鏡像磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. <span data-ttu-id="25984-248">在 hello**新增鏡像磁碟區**精靈頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="25984-248">On hello **New Mirrored Volume** wizard page, click **Next**.</span></span>
5. <span data-ttu-id="25984-249">在 hello**選取磁碟**頁面上，選取**磁碟 2**在 hello**選取** 窗格中，按一下**新增**，然後按一下**下一步**.</span><span class="sxs-lookup"><span data-stu-id="25984-249">On hello **Select Disks** page, select **Disk 2** in hello **Selected** pane, click **Add**, and then click **Next**.</span></span> 
6. <span data-ttu-id="25984-250">在 hello**指派磁碟機代號或路徑**頁面上，接受 hello 的預設值，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="25984-250">On hello **Assign Drive Letter or Path** page, accept hello defaults, and then click **Next**.</span></span> 
7. <span data-ttu-id="25984-251">在 hello**磁碟區格式化** 頁面的 hello**配置單位大小**方塊中，選取**64k**。</span><span class="sxs-lookup"><span data-stu-id="25984-251">On hello **Format Volume** page, in hello **Allocation Unit Size** box, select **64K**.</span></span> <span data-ttu-id="25984-252">選取 hello**執行快速格式化**核取方塊，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="25984-252">Select hello **Perform a quick format** check box, and then click **Next**.</span></span> 
8. <span data-ttu-id="25984-253">在 hello**完成 hello 新增鏡像磁碟區**頁面上，檢閱您的設定，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="25984-253">On hello **Completing hello New Mirrored Volume** page, review your settings, and then click **Finish**.</span></span> 
9. <span data-ttu-id="25984-254">Hello 基本磁碟的 tooindicate 才會轉換的 tooa 動態磁碟會出現訊息。</span><span class="sxs-lookup"><span data-stu-id="25984-254">A message appears tooindicate that hello basic disk will be converted tooa dynamic disk.</span></span> <span data-ttu-id="25984-255">按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="25984-255">Click **Yes**.</span></span>
   
    ![動態磁碟轉換訊息](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. <span data-ttu-id="25984-257">在磁碟管理中，確認磁碟區 1 與磁碟區 2 顯示為動態鏡像磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-257">In Disk Management, verify that Disk 1 and Disk 2 are shown as dynamic mirrored volumes.</span></span> <span data-ttu-id="25984-258">(**動態**應該出現在 hello 狀態 資料行，而且 hello 容量列顏色應變成 toored，指出鏡像磁碟區。)</span><span class="sxs-lookup"><span data-stu-id="25984-258">(**Dynamic** should appear in hello status column, and hello capacity bar color should change toored, indicating a mirrored volume.)</span></span> 
    
    ![磁碟管理的鏡像動態磁碟](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a><span data-ttu-id="25984-260">步驟 2： 使用 StorSimple Snapshot Manager tooconfigure 備份</span><span class="sxs-lookup"><span data-stu-id="25984-260">Step 2: Use StorSimple Snapshot Manager tooconfigure backup</span></span>
<span data-ttu-id="25984-261">使用下列程序 tooconfigure 動態鏡像磁碟區的 hello 然後立即啟動備份，或建立排定的備份原則。</span><span class="sxs-lookup"><span data-stu-id="25984-261">Use hello following procedure tooconfigure a dynamic mirrored volume, and then either start a backup immediately or create a policy for scheduled backups.</span></span>

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a><span data-ttu-id="25984-262">動態鏡像磁碟區的 tooconfigure 備份</span><span class="sxs-lookup"><span data-stu-id="25984-262">tooconfigure backup of a dynamic mirrored volume</span></span>
1. <span data-ttu-id="25984-263">按一下桌面上的 hello StorSimple Snapshot Manager 圖示。</span><span class="sxs-lookup"><span data-stu-id="25984-263">Click hello StorSimple Snapshot Manager icon on your desktop.</span></span> <span data-ttu-id="25984-264">hello StorSimple Snapshot Manager 視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="25984-264">hello StorSimple Snapshot Manager window appears.</span></span> 
2. <span data-ttu-id="25984-265">在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**磁碟區**節點，然後選取**重新掃描磁碟區**。</span><span class="sxs-lookup"><span data-stu-id="25984-265">In hello **Scope** pane, right-click hello **Volumes** node and select **Rescan volumes**.</span></span> <span data-ttu-id="25984-266">Hello 掃描完成時，磁碟區清單應該會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="25984-266">When hello scan is finished, a list of volumes should appear in hello **Results** pane.</span></span> <span data-ttu-id="25984-267">hello 動態鏡像磁碟區會列示為單一磁碟區。</span><span class="sxs-lookup"><span data-stu-id="25984-267">hello dynamic mirrored volume is listed as a single volume.</span></span> 
3. <span data-ttu-id="25984-268">在 [hello**結果**] 窗格中，hello 動態的鏡像磁碟區上按一下滑鼠右鍵，然後按一下**建立磁碟區群組**。</span><span class="sxs-lookup"><span data-stu-id="25984-268">In hello **Results** pane, right-click hello dynamic mirrored volume, and then click **Create Volume Group**.</span></span> 
4. <span data-ttu-id="25984-269">在 hello**建立磁碟區群組**對話方塊中，輸入 hello 磁碟區群組的名稱，指派 hello 動態鏡像磁碟區 toothis 群組，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="25984-269">In hello **Create Volume Group** dialog box, type a name for hello volume group, assign hello dynamic mirrored volume toothis group, and then click **OK**.</span></span> 
5. <span data-ttu-id="25984-270">在 [hello**範圍**] 窗格中，展開 hello**磁碟區群組**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-270">In hello **Scope** pane, expand hello **Volume Groups** node.</span></span> <span data-ttu-id="25984-271">hello 新磁碟區群組應該會出現在 hello**磁碟區群組**節點。</span><span class="sxs-lookup"><span data-stu-id="25984-271">hello new volume group should appear under hello  **Volume Groups** node.</span></span> 
6. <span data-ttu-id="25984-272">以滑鼠右鍵按一下 hello 磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="25984-272">Right-click hello volume group name.</span></span> 
   
   * <span data-ttu-id="25984-273">按一下 toostart 互動式 （隨） 備份工作，**取得備份**。</span><span class="sxs-lookup"><span data-stu-id="25984-273">toostart an interactive (on-demand) backup job, click **Take Backup**.</span></span> 
   * <span data-ttu-id="25984-274">tooschedule 的自動備份中，按一下**建立備份原則**。</span><span class="sxs-lookup"><span data-stu-id="25984-274">tooschedule an automatic backup, click **Create Backup Policy**.</span></span> <span data-ttu-id="25984-275">在 hello**一般**頁面上，選取 hello hello 清單中的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="25984-275">On hello **General** page, select hello volume group from hello list.</span></span> <span data-ttu-id="25984-276">在 hello**排程**頁面上，輸入 hello 排程詳細資料。</span><span class="sxs-lookup"><span data-stu-id="25984-276">On hello **Schedule** page, enter hello schedule details.</span></span> <span data-ttu-id="25984-277">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="25984-277">When you are finished, click **OK**.</span></span> 
7. <span data-ttu-id="25984-278">當它執行時，您可以監視 hello 備份工作。</span><span class="sxs-lookup"><span data-stu-id="25984-278">You can monitor hello backup job as it runs.</span></span> <span data-ttu-id="25984-279">在 hello**範圍** 窗格中，展開 hello**作業**節點，然後再按一下**執行**，hello 工作詳細資料會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="25984-279">In hello **Scope** pane, expand hello **Jobs** node, and then click **Running**, hello job details appear in hello **Results** pane.</span></span> <span data-ttu-id="25984-280">Hello 詳細資料 hello 備份工作完成時，會傳送的 toohello**過去 24**小時作業清單。</span><span class="sxs-lookup"><span data-stu-id="25984-280">When hello backup job is finished, hello details are transferred toohello **Last 24** hours job list.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="25984-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="25984-281">Next steps</span></span>
* <span data-ttu-id="25984-282">了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="25984-282">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="25984-283">了解如何太[使用 StorSimple Snapshot Manager toocreate 及管理磁碟區群組](storsimple-snapshot-manager-manage-volume-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="25984-283">Learn how too[use StorSimple Snapshot Manager toocreate and manage volume groups](storsimple-snapshot-manager-manage-volume-groups.md).</span></span>

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
