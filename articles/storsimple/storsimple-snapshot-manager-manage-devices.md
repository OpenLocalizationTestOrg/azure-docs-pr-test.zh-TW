---
title: "aaaManage 裝置與 StorSimple Snapshot Manager |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooconnect 和管理 StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a><span data-ttu-id="5332d-103">使用 StorSimple Snapshot Manager tooconnect 和管理 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-103">Use StorSimple Snapshot Manager tooconnect and manage StorSimple devices</span></span>
## <a name="overview"></a><span data-ttu-id="5332d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5332d-104">Overview</span></span>
<span data-ttu-id="5332d-105">您可以使用節點中 hello StorSimple Snapshot Manager**範圍**窗格 tooverify 匯入的 StorSimple 裝置資料和重新整理已連線的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-105">You can use nodes in hello StorSimple Snapshot Manager **Scope** pane tooverify imported StorSimple device data and refresh connected storage devices.</span></span> <span data-ttu-id="5332d-106">此外，當您按一下 hello**裝置** 節點，您可以看到一份連接的裝置和對應的狀態資訊在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="5332d-106">Additionally, when you click hello **Devices** node, you can see a list of connected devices and corresponding status information in hello **Results** pane.</span></span>

![連接的裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

<span data-ttu-id="5332d-108">**圖 1：StorSimple Snapshot Manager 連接的裝置**</span><span class="sxs-lookup"><span data-stu-id="5332d-108">**Figure 1: StorSimple Snapshot Manager connected device**</span></span> 

<span data-ttu-id="5332d-109">取決於您**檢視**選取項目、 hello**結果** 窗格會顯示 hello 下列每個裝置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5332d-109">Depending on your **View** selections, hello **Results** pane shows hello following information about each device.</span></span> <span data-ttu-id="5332d-110">(如需有關如何設定檢視的詳細資訊，請移至太[檢視 功能表](storsimple-use-snapshot-manager.md#view-menu)。</span><span class="sxs-lookup"><span data-stu-id="5332d-110">(For more information about configuring a view, go too[View menu](storsimple-use-snapshot-manager.md#view-menu).</span></span>

| <span data-ttu-id="5332d-111">結果資料行</span><span class="sxs-lookup"><span data-stu-id="5332d-111">Results column</span></span> | <span data-ttu-id="5332d-112">說明</span><span class="sxs-lookup"><span data-stu-id="5332d-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="5332d-113">名稱</span><span class="sxs-lookup"><span data-stu-id="5332d-113">Name</span></span> |<span data-ttu-id="5332d-114">hello hello 裝置 hello Azure 傳統入口網站中的設定名稱</span><span class="sxs-lookup"><span data-stu-id="5332d-114">hello name of hello device as configured in hello Azure classic portal</span></span> |
| <span data-ttu-id="5332d-115">模型</span><span class="sxs-lookup"><span data-stu-id="5332d-115">Model</span></span> |<span data-ttu-id="5332d-116">hello 裝置 hello 型號號碼</span><span class="sxs-lookup"><span data-stu-id="5332d-116">hello model number of hello device</span></span> |
| <span data-ttu-id="5332d-117">版本</span><span class="sxs-lookup"><span data-stu-id="5332d-117">Version</span></span> |<span data-ttu-id="5332d-118">hello 新版 hello hello 裝置上安裝的軟體</span><span class="sxs-lookup"><span data-stu-id="5332d-118">hello version of hello software installed on hello device</span></span> |
| <span data-ttu-id="5332d-119">狀態</span><span class="sxs-lookup"><span data-stu-id="5332d-119">Status</span></span> |<span data-ttu-id="5332d-120">Hello 裝置是否可供使用</span><span class="sxs-lookup"><span data-stu-id="5332d-120">Whether hello device is available</span></span> |
| <span data-ttu-id="5332d-121">上次同步處理</span><span class="sxs-lookup"><span data-stu-id="5332d-121">Last Synced</span></span> |<span data-ttu-id="5332d-122">日期和時間時 hello 裝置上次同步處理</span><span class="sxs-lookup"><span data-stu-id="5332d-122">Date and time when hello device was last synchronized</span></span> |
| <span data-ttu-id="5332d-123">序號</span><span class="sxs-lookup"><span data-stu-id="5332d-123">Serial No.</span></span> |<span data-ttu-id="5332d-124">hello 裝置 hello 序號</span><span class="sxs-lookup"><span data-stu-id="5332d-124">hello serial number for hello device</span></span> |

<span data-ttu-id="5332d-125">如果您以滑鼠右鍵按一下 hello**裝置**hello 中的節點**範圍** 窗格中，您可以選取從 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="5332d-125">If you right-click hello **Devices** node in hello **Scope** pane, you can select from hello following actions:</span></span>

* <span data-ttu-id="5332d-126">新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-126">Add or replace a device</span></span>
* <span data-ttu-id="5332d-127">連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="5332d-127">Connect a device and verify imports</span></span>
* <span data-ttu-id="5332d-128">重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-128">Refresh connected devices</span></span>

<span data-ttu-id="5332d-129">如果您按一下 hello**裝置**hello 中的節點，然後以滑鼠右鍵按一下裝置名稱**結果** 窗格中，您可以選取從 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="5332d-129">If you click hello **Devices** node and then right-click a device name in hello **Results** pane, you can select from hello following actions:</span></span>

* <span data-ttu-id="5332d-130">驗證裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-130">Authenticate a device</span></span>
* <span data-ttu-id="5332d-131">檢視裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="5332d-131">View device details</span></span>
* <span data-ttu-id="5332d-132">重新整理裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-132">Refresh a device</span></span>
* <span data-ttu-id="5332d-133">刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="5332d-133">Delete a device configuration</span></span>
* <span data-ttu-id="5332d-134">變更裝置密碼</span><span class="sxs-lookup"><span data-stu-id="5332d-134">Change a device password</span></span>

> [!NOTE]
> <span data-ttu-id="5332d-135">所有這些動作也會提供在 hello**動作**窗格。</span><span class="sxs-lookup"><span data-stu-id="5332d-135">All of these actions are also available in hello **Actions** pane.</span></span>


<span data-ttu-id="5332d-136">本教學課程說明如何 toouse StorSimple Snapshot Manager tooconnect 及管理裝置，並執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="5332d-136">This tutorial explains how toouse StorSimple Snapshot Manager tooconnect and manage devices and perform hello following tasks:</span></span>

* <span data-ttu-id="5332d-137">新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-137">Add or replace a device</span></span>
* <span data-ttu-id="5332d-138">連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="5332d-138">Connect a device and verify imports</span></span>
* <span data-ttu-id="5332d-139">重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-139">Refresh connected devices</span></span>
* <span data-ttu-id="5332d-140">驗證裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-140">Authenticate a device</span></span>
* <span data-ttu-id="5332d-141">檢視裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="5332d-141">View device details</span></span>
* <span data-ttu-id="5332d-142">重新整理個別裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-142">Refresh an individual device</span></span>
* <span data-ttu-id="5332d-143">刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="5332d-143">Delete a device configuration</span></span>
* <span data-ttu-id="5332d-144">變更過期的裝置密碼</span><span class="sxs-lookup"><span data-stu-id="5332d-144">Change an expired device password</span></span>
* <span data-ttu-id="5332d-145">更換故障的裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-145">Replace a failed device</span></span>

> [!NOTE]
> <span data-ttu-id="5332d-146">如需使用 hello StorSimple Snapshot Manager 介面的一般資訊，請移太[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5332d-146">For general information about using hello StorSimple Snapshot Manager interface, go too[StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>


## <a name="add-or-replace-a-device"></a><span data-ttu-id="5332d-147">新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-147">Add or replace a device</span></span>
<span data-ttu-id="5332d-148">使用下列程序 tooadd hello 或取代 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-148">Use hello following procedure tooadd or replace a StorSimple device.</span></span>

#### <a name="tooadd-or-replace-a-device"></a><span data-ttu-id="5332d-149">tooadd 或取代裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-149">tooadd or replace a device</span></span>
1. <span data-ttu-id="5332d-150">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-150">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="5332d-151">在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**裝置**節點，然後再按一下**設定裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-151">In hello **Scope** pane, right-click hello **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="5332d-152">hello**設定裝置** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5332d-152">hello **Configure a Device** dialog box appears.</span></span>
   
    ![設定 StorSimple 裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. <span data-ttu-id="5332d-154">在 hello**裝置**下拉式清單方塊中，選取 hello hello 裝置或虛擬裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5332d-154">In hello **Device** drop-down box, select hello IP address of hello device or virtual device.</span></span> 
4. <span data-ttu-id="5332d-155">在 hello**密碼**文字方塊中，您建立 hello 裝置 hello Azure 傳統入口網站中的型別 hello StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="5332d-155">In hello **Password** text box, type hello StorSimple Snapshot Manager password that you created for hello device in hello Azure classic portal.</span></span> <span data-ttu-id="5332d-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5332d-156">Click **OK**.</span></span> <span data-ttu-id="5332d-157">StorSimple Snapshot Manager 搜尋您所識別的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-157">StorSimple Snapshot Manager searches for hello device that you identified.</span></span> 
   
   * <span data-ttu-id="5332d-158">如果使用 hello 裝置，StorSimple Snapshot Manager 就會加入連接。</span><span class="sxs-lookup"><span data-stu-id="5332d-158">If hello device is available, StorSimple Snapshot Manager adds a connection.</span></span>
   * <span data-ttu-id="5332d-159">如果因為任何原因無法使用 hello 裝置，StorSimple Snapshot Manager 就會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5332d-159">If hello device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="5332d-160">按一下**確定**tooclose hello 錯誤訊息，然後按一下**取消**tooclose hello**設定裝置** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5332d-160">Click **OK** tooclose hello error message, and then click **Cancel** tooclose hello **Configure a Device** dialog box.</span></span>

## <a name="connect-a-device-and-verify-imports"></a><span data-ttu-id="5332d-161">連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="5332d-161">Connect a device and verify imports</span></span>
<span data-ttu-id="5332d-162">使用下列程序 tooconnect StorSimple 裝置 hello，並確認具備相關聯備份任何現有磁碟區群組匯入。</span><span class="sxs-lookup"><span data-stu-id="5332d-162">Use hello following procedure tooconnect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span></span>

#### <a name="tooconnect-a-device-and-verify-imports"></a><span data-ttu-id="5332d-163">tooconnect 裝置並驗證匯入</span><span class="sxs-lookup"><span data-stu-id="5332d-163">tooconnect a device and verify imports</span></span>
1. <span data-ttu-id="5332d-164">tooconnect 裝置 tooStorSimple Snapshot Manager 遵循 hello 指示中新增或取代裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-164">tooconnect a device tooStorSimple Snapshot Manager, follow hello instructions in Add or replace a device.</span></span> <span data-ttu-id="5332d-165">當它連接 tooa 裝置時，StorSimple Snapshot Manager 回應，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5332d-165">When it connects tooa device, StorSimple Snapshot Manager responds as follows:</span></span>
   
   * <span data-ttu-id="5332d-166">如果因為任何原因無法使用 hello 裝置，StorSimple Snapshot Manager 就會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5332d-166">If hello device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> 
   
   * <span data-ttu-id="5332d-167">如果使用 hello 裝置，StorSimple Snapshot Manager 就會加入連接。</span><span class="sxs-lookup"><span data-stu-id="5332d-167">If hello device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="5332d-168">當您選取 hello 裝置時，它會出現在 hello**結果** 窗格中，而 hello 狀態欄位表示該 hello 裝置為**可用**。</span><span class="sxs-lookup"><span data-stu-id="5332d-168">When you select hello device, it appears in hello **Results** pane, and hello status field indicates that hello device is **Available**.</span></span> <span data-ttu-id="5332d-169">StorSimple Snapshot Manager 匯入設定 hello 裝置的任何磁碟區群組，前提是 hello 磁碟區群組有相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="5332d-169">StorSimple Snapshot Manager imports any volume groups configured for hello device, provided that hello volume groups have associated backups.</span></span> <span data-ttu-id="5332d-170">不會匯入備份原則。</span><span class="sxs-lookup"><span data-stu-id="5332d-170">Backup policies are not imported.</span></span> <span data-ttu-id="5332d-171">不會匯入沒有相關聯備份的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="5332d-171">Volume groups that do not have associated backups are not imported.</span></span>
2. <span data-ttu-id="5332d-172">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-172">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
3. <span data-ttu-id="5332d-173">以滑鼠右鍵按一下 hello 中的最上層節點 hello**範圍** 窗格中，然後再按一下**切換匯入顯示**。</span><span class="sxs-lookup"><span data-stu-id="5332d-173">Right-click hello top node in hello **Scope** pane, and then click **Toggle Imports Display**.</span></span>
   
    ![選取 [切換匯入顯示]](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. <span data-ttu-id="5332d-175">hello**切換匯入顯示**磁碟區群組及備份時將會出現對話方塊，顯示 hello hello 狀態匯入。</span><span class="sxs-lookup"><span data-stu-id="5332d-175">hello **Toggle Imports Display** dialog box appears, showing hello status of hello imported volume groups and backups.</span></span> <span data-ttu-id="5332d-176">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5332d-176">Click **OK**.</span></span>

<span data-ttu-id="5332d-177">Hello 磁碟區群組及備份已順利匯入之後，您可以使用 StorSimple Snapshot Manager toomanage 它們，就如同您管理磁碟區群組及您建立及設定 StorSimple Snapshot Manager 使用的備份。</span><span class="sxs-lookup"><span data-stu-id="5332d-177">After hello volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager toomanage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span></span> 

## <a name="refresh-connected-devices"></a><span data-ttu-id="5332d-178">重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-178">Refresh connected devices</span></span>
<span data-ttu-id="5332d-179">使用下列程序 toosynchronize hello 連接 StorSimple 裝置的 StorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="5332d-179">Use hello following procedure toosynchronize hello connected StorSimple devices with StorSimple Snapshot Manager.</span></span>

#### <a name="toorefresh-connected-devices"></a><span data-ttu-id="5332d-180">toorefresh 連接的裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-180">toorefresh connected devices</span></span>
1. <span data-ttu-id="5332d-181">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-181">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="5332d-182">在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**裝置**，然後按一下**重新整理裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-182">In hello **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span></span> <span data-ttu-id="5332d-183">這會同步處理 hello 連接裝置與 StorSimple Snapshot Manager，讓您可以檢視 hello 磁碟區群組及備份，包括任何最近新增項目。</span><span class="sxs-lookup"><span data-stu-id="5332d-183">This synchronizes hello connected devices with StorSimple Snapshot Manager so that you can view hello volume groups and backups, including any recent additions.</span></span> 
   
    ![重新整理 hello StorSimple 裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

<span data-ttu-id="5332d-185">hello**重新整理裝置**動作會擷取任何新的磁碟區群組及任何相關聯的備份從連接的裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-185">hello **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span></span> <span data-ttu-id="5332d-186">不同於 hello**重新掃描磁碟區**動作供 hello**磁碟區** 節點，**重新整理裝置**不會還原 hello 備份登錄。</span><span class="sxs-lookup"><span data-stu-id="5332d-186">Unlike hello **Rescan volumes** action available for hello **Volumes** node, **Refresh Devices** does not restore hello backup registry.</span></span>

## <a name="authenticate-a-device"></a><span data-ttu-id="5332d-187">驗證裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-187">Authenticate a device</span></span>
<span data-ttu-id="5332d-188">使用下列程序 tooauthenticate StorSimple 裝置的 StorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="5332d-188">Use hello following procedure tooauthenticate a StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="tooauthenticate-a-device"></a><span data-ttu-id="5332d-189">tooauthenticate 裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-189">tooauthenticate a device</span></span>
1. <span data-ttu-id="5332d-190">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-190">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="5332d-191">在 hello**範圍** 窗格中，按一下 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-191">In hello **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="5332d-192">在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**驗證**。</span><span class="sxs-lookup"><span data-stu-id="5332d-192">In hello **Results** pane, right-click hello name of hello device, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="5332d-193">hello**驗證** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5332d-193">hello **Authenticate** dialog box appears.</span></span> <span data-ttu-id="5332d-194">輸入 hello 裝置密碼，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5332d-194">Type hello device password, and then click **OK**.</span></span>
   
    ![[驗證] 對話方塊](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a><span data-ttu-id="5332d-196">檢視裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="5332d-196">View device details</span></span>
<span data-ttu-id="5332d-197">使用下列程序 tooview hello 詳細資料的 StorSimple 裝置 hello，並視需要重新同步處理 hello 裝置與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-197">Use hello following procedure tooview hello details of a StorSimple device and, if necessary, resynchronize hello device with StorSimple Snapshot Manager.</span></span>

#### <a name="tooview-and-resynchronize-device-details"></a><span data-ttu-id="5332d-198">tooview 和重新同步處理裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="5332d-198">tooview and resynchronize device details</span></span>
1. <span data-ttu-id="5332d-199">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-199">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="5332d-200">在 hello**範圍** 窗格中，按一下 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-200">In hello **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="5332d-201">在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="5332d-201">In hello **Results** pane, right-click hello name of hello device, and then click **Details**.</span></span>

<span data-ttu-id="5332d-202">4.hello**裝置詳細資料** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5332d-202">4.hello **Device Details** dialog box appears.</span></span> <span data-ttu-id="5332d-203">此方塊會顯示 hello 名稱、 模型、 版本、 序號、 狀態、 目標 iSCSI 合格名稱 (IQN) 及上次同步處理日期和時間。</span><span class="sxs-lookup"><span data-stu-id="5332d-203">This box shows hello name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span></span>

* <span data-ttu-id="5332d-204">按一下**重新同步處理**toosynchronize hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-204">Click **Resync** toosynchronize hello device.</span></span>
* <span data-ttu-id="5332d-205">按一下**確定**或**取消**tooclose hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5332d-205">Click **OK** or **Cancel** tooclose hello dialog box.</span></span>
  
  ![裝置詳細資料](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a><span data-ttu-id="5332d-207">重新整理個別裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-207">Refresh an individual device</span></span>
<span data-ttu-id="5332d-208">使用下列程序 tooresynchronize 個別的 StorSimple 裝置的 StorSimple Snapshot Manager hello。</span><span class="sxs-lookup"><span data-stu-id="5332d-208">Use hello following procedure tooresynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="toorefresh-a-device"></a><span data-ttu-id="5332d-209">toorefresh 裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-209">toorefresh a device</span></span>
1. <span data-ttu-id="5332d-210">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-210">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="5332d-211">在 hello**範圍** 窗格中，按一下 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-211">In hello **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="5332d-212">在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**重新整理裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-212">In hello **Results** pane, right-click hello name of hello device, and then click **Refresh Device**.</span></span> <span data-ttu-id="5332d-213">此同步處理裝置 hello 與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-213">This synchronizes hello device with StorSimple Snapshot Manager.</span></span>

## <a name="delete-a-device-configuration"></a><span data-ttu-id="5332d-214">刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="5332d-214">Delete a device configuration</span></span>
<span data-ttu-id="5332d-215">使用下列程序 toodelete 個別的 StorSimple 裝置設定 StorSimple Snapshot Manager 從 hello。</span><span class="sxs-lookup"><span data-stu-id="5332d-215">Use hello following procedure toodelete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span></span>

#### <a name="toodelete-a-device-configuration"></a><span data-ttu-id="5332d-216">toodelete 裝置組態</span><span class="sxs-lookup"><span data-stu-id="5332d-216">toodelete a device configuration</span></span>
1. <span data-ttu-id="5332d-217">按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-217">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="5332d-218">在 hello**範圍** 窗格中，按一下 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-218">In hello **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="5332d-219">在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="5332d-219">In hello **Results** pane, right-click hello name of hello device, and then click **Delete**.</span></span> 
4. <span data-ttu-id="5332d-220">hello 下訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="5332d-220">hello following message appears.</span></span> <span data-ttu-id="5332d-221">按一下**是**toodelete hello 組態，或按一下**否**toocancel hello 刪除。</span><span class="sxs-lookup"><span data-stu-id="5332d-221">Click **Yes** toodelete hello configuration or click **No** toocancel hello deletion.</span></span>
   
    ![刪除裝置組態](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a><span data-ttu-id="5332d-223">變更過期的裝置密碼</span><span class="sxs-lookup"><span data-stu-id="5332d-223">Change an expired device password</span></span>
<span data-ttu-id="5332d-224">您必須輸入密碼 tooauthenticate StorSimple 裝置的 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-224">You must enter a password tooauthenticate a StorSimple device with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5332d-225">當您使用 hello Windows PowerShell 介面 tooset hello 裝置時，您可以設定這個密碼。</span><span class="sxs-lookup"><span data-stu-id="5332d-225">You configure this password when you use hello Windows PowerShell interface tooset up hello device.</span></span> <span data-ttu-id="5332d-226">不過，hello 密碼可能會過期。</span><span class="sxs-lookup"><span data-stu-id="5332d-226">However, hello password can expire.</span></span> <span data-ttu-id="5332d-227">如果發生這種情況，您可以使用 hello Azure 傳統入口網站 toochange hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="5332d-227">If this happens, you can use hello Azure classic portal toochange hello password.</span></span> <span data-ttu-id="5332d-228">然後，因為 hello 裝置已設定 StorSimple Snapshot Manager 中的 hello 密碼過期之前，您必須重新驗證 hello 裝置在 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-228">Then, because hello device was configured in StorSimple Snapshot Manager before hello password expired, you must re-authenticate hello device in StorSimple Snapshot Manager.</span></span>

#### <a name="toochange-hello-expired-password"></a><span data-ttu-id="5332d-229">toochange hello 過期的密碼</span><span class="sxs-lookup"><span data-stu-id="5332d-229">toochange hello expired password</span></span>
1. <span data-ttu-id="5332d-230">在 hello Azure 傳統入口網站，開始 hello StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="5332d-230">In hello Azure classic portal, start hello StorSimple Manager service.</span></span>
2. <span data-ttu-id="5332d-231">按一下**裝置** > **設定**hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-231">Click **Devices** > **Configure** for hello device.</span></span>
3. <span data-ttu-id="5332d-232">捲動 toohello StorSimple Snapshot Manager > 一節。</span><span class="sxs-lookup"><span data-stu-id="5332d-232">Scroll down toohello StorSimple Snapshot Manager section.</span></span> <span data-ttu-id="5332d-233">輸入 14 或 15 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="5332d-233">Enter a password that is 14-15 characters.</span></span> <span data-ttu-id="5332d-234">請確定該 hello 密碼包含大寫、 小寫、 數字及特殊字元的混合。</span><span class="sxs-lookup"><span data-stu-id="5332d-234">Make sure that hello password contains a mix of uppercase, lowercase, numeric, and special characters.</span></span>
4. <span data-ttu-id="5332d-235">重新輸入 hello 密碼 tooconfirm 它。</span><span class="sxs-lookup"><span data-stu-id="5332d-235">Re-enter hello password tooconfirm it.</span></span>
5. <span data-ttu-id="5332d-236">按一下**儲存**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="5332d-236">Click **Save** at hello bottom of hello page.</span></span>

#### <a name="toore-authenticate-hello-device"></a><span data-ttu-id="5332d-237">toore-驗證 hello 裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-237">toore-authenticate hello device</span></span>
1. <span data-ttu-id="5332d-238">啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-238">Start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="5332d-239">在 hello**範圍** 窗格中，按一下 **裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-239">In hello **Scope** pane, click **Devices**.</span></span> <span data-ttu-id="5332d-240">設定裝置的清單會出現在 hello**結果**窗格。</span><span class="sxs-lookup"><span data-stu-id="5332d-240">A list of configured devices appears in hello **Results** pane.</span></span>
3. <span data-ttu-id="5332d-241">選取裝置 hello、 按一下滑鼠右鍵，然後按一下**驗證**。</span><span class="sxs-lookup"><span data-stu-id="5332d-241">Select hello device, right-click, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="5332d-242">在 hello**驗證**視窗中，輸入 hello 新密碼。</span><span class="sxs-lookup"><span data-stu-id="5332d-242">In hello **Authenticate** window, enter hello new password.</span></span>
5. <span data-ttu-id="5332d-243">選取 hello 裝置，以滑鼠右鍵按一下，並選取**重新整理裝置**。</span><span class="sxs-lookup"><span data-stu-id="5332d-243">Select hello device, right-click, and select **Refresh device**.</span></span> <span data-ttu-id="5332d-244">此同步處理裝置 hello 與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-244">This synchronizes hello device with StorSimple Snapshot Manager.</span></span>

## <a name="replace-a-failed-device"></a><span data-ttu-id="5332d-245">更換故障的裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-245">Replace a failed device</span></span>
<span data-ttu-id="5332d-246">如果 StorSimple 裝置故障，並由備用 （容錯移轉） 裝置，使用下列步驟 tooconnect 的 hello 取代 toohello 新裝置和檢視 hello 相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="5332d-246">If a StorSimple device fails and is replaced by a standby (failover) device, use hello following steps tooconnect toohello new device and view hello associated backups.</span></span>

#### <a name="tooconnect-tooa-new-device-after-failover"></a><span data-ttu-id="5332d-247">在容錯移轉之後 tooconnect tooa 新裝置</span><span class="sxs-lookup"><span data-stu-id="5332d-247">tooconnect tooa new device after failover</span></span>
1. <span data-ttu-id="5332d-248">重新設定 hello iSCSI 連線 toohello 新裝置。</span><span class="sxs-lookup"><span data-stu-id="5332d-248">Reconfigure hello iSCSI connection toohello new device.</span></span> <span data-ttu-id="5332d-249">如需相關指示，請移至太 」 步驟 7： 掛接、 初始化、 和格式的磁碟區 」 中[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="5332d-249">For instructions, go too"Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5332d-250">如果新 StorSimple 裝置 hello 具有舊 hello hello 相同的 IP 位址，您可能會無法 tooconnect hello 舊組態。</span><span class="sxs-lookup"><span data-stu-id="5332d-250">If hello new StorSimple device has hello same IP address as hello old one, you might be able tooconnect hello old configuration.</span></span>


1. <span data-ttu-id="5332d-251">停止 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="5332d-251">Stop hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="5332d-252">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="5332d-252">Start Server Manager.</span></span>
   2. <span data-ttu-id="5332d-253">在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="5332d-253">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="5332d-254">在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="5332d-254">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="5332d-255">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。</span><span class="sxs-lookup"><span data-stu-id="5332d-255">In hello right pane, under **Microsoft StorSimple Management Service**, click **Stop hello service**.</span></span>
2. <span data-ttu-id="5332d-256">移除 hello 組態資訊相關的 toohello 舊裝置：</span><span class="sxs-lookup"><span data-stu-id="5332d-256">Remove hello configuration information related toohello old device:</span></span>
   
   1. <span data-ttu-id="5332d-257">在檔案總管 中，瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。</span><span class="sxs-lookup"><span data-stu-id="5332d-257">In File Explorer, browse tooC:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   2. <span data-ttu-id="5332d-258">刪除 hello BACatalog 資料夾中的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5332d-258">Delete hello files in hello BACatalog folder.</span></span>
3. <span data-ttu-id="5332d-259">重新啟動 Microsoft StorSimple 管理服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="5332d-259">Restart hello Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="5332d-260">在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。</span><span class="sxs-lookup"><span data-stu-id="5332d-260">On hello Server Manager Dashboard, on hello **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="5332d-261">在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。</span><span class="sxs-lookup"><span data-stu-id="5332d-261">On hello **Services** window, select hello **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="5332d-262">在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。</span><span class="sxs-lookup"><span data-stu-id="5332d-262">In hello right pane, under **Microsoft StorSimple Management Service**, click **Restart hello service**.</span></span>
4. <span data-ttu-id="5332d-263">啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="5332d-263">Start StorSimple Snapshot Manager.</span></span>
5. <span data-ttu-id="5332d-264">tooconfigure hello 新 StorSimple 裝置，請完成 hello 步驟在步驟 2： 連接 StorSimple 裝置中的[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="5332d-264">tooconfigure hello new StorSimple device, complete hello steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
6. <span data-ttu-id="5332d-265">以滑鼠右鍵按一下 hello 中的最上層節點 hello**範圍**窗格 (StorSimple Snapshot Manager hello 範例，)，然後按一下**切換匯入顯示**。</span><span class="sxs-lookup"><span data-stu-id="5332d-265">Right-click hello top-level node in hello **Scope** pane (StorSimple Snapshot Manager in hello example), and then click **Toggle Imports Display**.</span></span> 
7. <span data-ttu-id="5332d-266">Hello 匯入磁碟區群組，並備份會顯示在 StorSimple Snapshot Manager 時，就會出現訊息。</span><span class="sxs-lookup"><span data-stu-id="5332d-266">A message appears when hello imported volume groups and backups are visible in StorSimple Snapshot Manager.</span></span> <span data-ttu-id="5332d-267">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="5332d-267">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5332d-268">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5332d-268">Next steps</span></span>
* <span data-ttu-id="5332d-269">了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="5332d-269">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="5332d-270">了解如何太[使用 StorSimple Snapshot Manager tooview 及管理磁碟區](storsimple-snapshot-manager-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="5332d-270">Learn how too[use StorSimple Snapshot Manager tooview and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span></span>

