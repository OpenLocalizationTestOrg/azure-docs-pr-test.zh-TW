---
title: "使用 StorSimple Snapshot Manager 來管理裝置 | Microsoft Docs"
description: "描述如何使用 StorSimple Snapshot Manager MMC 嵌入式管理單元，來連接和管理 StorSimple 裝置。"
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
ms.openlocfilehash: f5e3186a4271e0be781f367fa75ada195c58c960
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-connect-and-manage-storsimple-devices"></a><span data-ttu-id="ecdcb-103">使用 StorSimple Snapshot Manager 來連接和管理 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-103">Use StorSimple Snapshot Manager to connect and manage StorSimple devices</span></span>
## <a name="overview"></a><span data-ttu-id="ecdcb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="ecdcb-104">Overview</span></span>
<span data-ttu-id="ecdcb-105">您可以使用 StorSimple Snapshot Manager [ **範圍** ] 窗格中的節點，來確認已匯入的 StorSimple 裝置資料，並重新整理已連接的儲存體裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-105">You can use nodes in the StorSimple Snapshot Manager **Scope** pane to verify imported StorSimple device data and refresh connected storage devices.</span></span> <span data-ttu-id="ecdcb-106">此外，當您按一下 [裝置] 節點時，也可以在 [結果] 窗格中看到已連接的裝置清單和對應的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-106">Additionally, when you click the **Devices** node, you can see a list of connected devices and corresponding status information in the **Results** pane.</span></span>

![連接的裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

<span data-ttu-id="ecdcb-108">**圖 1：StorSimple Snapshot Manager 連接的裝置**</span><span class="sxs-lookup"><span data-stu-id="ecdcb-108">**Figure 1: StorSimple Snapshot Manager connected device**</span></span> 

<span data-ttu-id="ecdcb-109">視您的 [檢視] 選項而定，[結果] 窗格會顯示每個裝置的下列相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-109">Depending on your **View** selections, the **Results** pane shows the following information about each device.</span></span> <span data-ttu-id="ecdcb-110">(如需設定檢視的詳細資訊，請移至 [檢視功能表](storsimple-use-snapshot-manager.md#view-menu)。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-110">(For more information about configuring a view, go to [View menu](storsimple-use-snapshot-manager.md#view-menu).</span></span>

| <span data-ttu-id="ecdcb-111">結果資料行</span><span class="sxs-lookup"><span data-stu-id="ecdcb-111">Results column</span></span> | <span data-ttu-id="ecdcb-112">說明</span><span class="sxs-lookup"><span data-stu-id="ecdcb-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ecdcb-113">名稱</span><span class="sxs-lookup"><span data-stu-id="ecdcb-113">Name</span></span> |<span data-ttu-id="ecdcb-114">Azure 傳統入口網站中設定的裝置名稱</span><span class="sxs-lookup"><span data-stu-id="ecdcb-114">The name of the device as configured in the Azure classic portal</span></span> |
| <span data-ttu-id="ecdcb-115">模型</span><span class="sxs-lookup"><span data-stu-id="ecdcb-115">Model</span></span> |<span data-ttu-id="ecdcb-116">裝置的型號</span><span class="sxs-lookup"><span data-stu-id="ecdcb-116">The model number of the device</span></span> |
| <span data-ttu-id="ecdcb-117">版本</span><span class="sxs-lookup"><span data-stu-id="ecdcb-117">Version</span></span> |<span data-ttu-id="ecdcb-118">裝置上安裝的軟體版本</span><span class="sxs-lookup"><span data-stu-id="ecdcb-118">The version of the software installed on the device</span></span> |
| <span data-ttu-id="ecdcb-119">Status</span><span class="sxs-lookup"><span data-stu-id="ecdcb-119">Status</span></span> |<span data-ttu-id="ecdcb-120">裝置是否可用</span><span class="sxs-lookup"><span data-stu-id="ecdcb-120">Whether the device is available</span></span> |
| <span data-ttu-id="ecdcb-121">上次同步處理</span><span class="sxs-lookup"><span data-stu-id="ecdcb-121">Last Synced</span></span> |<span data-ttu-id="ecdcb-122">上次同步處理裝置的日期和時間時</span><span class="sxs-lookup"><span data-stu-id="ecdcb-122">Date and time when the device was last synchronized</span></span> |
| <span data-ttu-id="ecdcb-123">序號</span><span class="sxs-lookup"><span data-stu-id="ecdcb-123">Serial No.</span></span> |<span data-ttu-id="ecdcb-124">裝置的序號</span><span class="sxs-lookup"><span data-stu-id="ecdcb-124">The serial number for the device</span></span> |

<span data-ttu-id="ecdcb-125">如果您以滑鼠右鍵按一下 [範圍] 窗格中的 [裝置] 節點，則可以選取下列動作：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-125">If you right-click the **Devices** node in the **Scope** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="ecdcb-126">新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-126">Add or replace a device</span></span>
* <span data-ttu-id="ecdcb-127">連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="ecdcb-127">Connect a device and verify imports</span></span>
* <span data-ttu-id="ecdcb-128">重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-128">Refresh connected devices</span></span>

<span data-ttu-id="ecdcb-129">如果您按一下 [裝置] 節點，然後再以滑鼠右鍵按一下 [結果] 窗格中的裝置名稱，則可以選取下列動作：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-129">If you click the **Devices** node and then right-click a device name in the **Results** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="ecdcb-130">驗證裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-130">Authenticate a device</span></span>
* <span data-ttu-id="ecdcb-131">檢視裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="ecdcb-131">View device details</span></span>
* <span data-ttu-id="ecdcb-132">重新整理裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-132">Refresh a device</span></span>
* <span data-ttu-id="ecdcb-133">刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="ecdcb-133">Delete a device configuration</span></span>
* <span data-ttu-id="ecdcb-134">變更裝置密碼</span><span class="sxs-lookup"><span data-stu-id="ecdcb-134">Change a device password</span></span>

> [!NOTE]
> <span data-ttu-id="ecdcb-135">所有這些動作也可在 [ **動作** ] 窗格中取得。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-135">All of these actions are also available in the **Actions** pane.</span></span>


<span data-ttu-id="ecdcb-136">本教學課程說明如何使用 StorSimple Snapshot Manager，來連接和管理裝置，並執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-136">This tutorial explains how to use StorSimple Snapshot Manager to connect and manage devices and perform the following tasks:</span></span>

* <span data-ttu-id="ecdcb-137">新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-137">Add or replace a device</span></span>
* <span data-ttu-id="ecdcb-138">連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="ecdcb-138">Connect a device and verify imports</span></span>
* <span data-ttu-id="ecdcb-139">重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-139">Refresh connected devices</span></span>
* <span data-ttu-id="ecdcb-140">驗證裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-140">Authenticate a device</span></span>
* <span data-ttu-id="ecdcb-141">檢視裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="ecdcb-141">View device details</span></span>
* <span data-ttu-id="ecdcb-142">重新整理個別裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-142">Refresh an individual device</span></span>
* <span data-ttu-id="ecdcb-143">刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="ecdcb-143">Delete a device configuration</span></span>
* <span data-ttu-id="ecdcb-144">變更過期的裝置密碼</span><span class="sxs-lookup"><span data-stu-id="ecdcb-144">Change an expired device password</span></span>
* <span data-ttu-id="ecdcb-145">更換故障的裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-145">Replace a failed device</span></span>

> [!NOTE]
> <span data-ttu-id="ecdcb-146">如需使用 StorSimple Snapshot Manager 介面的一般資訊，請至 [StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-146">For general information about using the StorSimple Snapshot Manager interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>


## <a name="add-or-replace-a-device"></a><span data-ttu-id="ecdcb-147">新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-147">Add or replace a device</span></span>
<span data-ttu-id="ecdcb-148">請使用下列程序來新增或更換 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-148">Use the following procedure to add or replace a StorSimple device.</span></span>

#### <a name="to-add-or-replace-a-device"></a><span data-ttu-id="ecdcb-149">若要新增或更換裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-149">To add or replace a device</span></span>
1. <span data-ttu-id="ecdcb-150">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-150">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ecdcb-151">在 [範圍] 窗格中，以滑鼠右鍵按一下 [裝置] 節點，然後按一下 [設定裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-151">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="ecdcb-152">[ **設定裝置** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-152">The **Configure a Device** dialog box appears.</span></span>
   
    ![設定 StorSimple 裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. <span data-ttu-id="ecdcb-154">在 [ **裝置** ] 下拉式清單方塊中，選取裝置或虛擬裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-154">In the **Device** drop-down box, select the IP address of the device or virtual device.</span></span> 
4. <span data-ttu-id="ecdcb-155">在 [密碼]  文字方塊中，輸入您在 Azure 傳統入口網站中為裝置建立的 StorSimple Snapshot Manager 密碼。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-155">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure classic portal.</span></span> <span data-ttu-id="ecdcb-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-156">Click **OK**.</span></span> <span data-ttu-id="ecdcb-157">StorSimple Snapshot Manager 會搜尋您所識別的裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-157">StorSimple Snapshot Manager searches for the device that you identified.</span></span> 
   
   * <span data-ttu-id="ecdcb-158">如果裝置可用，StorSimple Snapshot Manager 會新增連接。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-158">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span>
   * <span data-ttu-id="ecdcb-159">如果由於任何原因而無法使用裝置，StorSimple Snapshot Manager 會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-159">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="ecdcb-160">按一下 [確定] 以關閉錯誤訊息，然後按一下 [取消] 以關閉 [設定裝置] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-160">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span></span>

## <a name="connect-a-device-and-verify-imports"></a><span data-ttu-id="ecdcb-161">連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="ecdcb-161">Connect a device and verify imports</span></span>
<span data-ttu-id="ecdcb-162">請使用下列程序來連接 StorSimple 裝置，並確認任何已匯入的現有磁碟區群組具有相關聯的備份，。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-162">Use the following procedure to connect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span></span>

#### <a name="to-connect-a-device-and-verify-imports"></a><span data-ttu-id="ecdcb-163">若要連接裝置並確認匯入</span><span class="sxs-lookup"><span data-stu-id="ecdcb-163">To connect a device and verify imports</span></span>
1. <span data-ttu-id="ecdcb-164">若要將裝置連接至 StorSimple Snapshot Manager，請遵循新增或更換裝置中的指示。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-164">To connect a device to StorSimple Snapshot Manager, follow the instructions in Add or replace a device.</span></span> <span data-ttu-id="ecdcb-165">當它連接至裝置時，StorSimple Snapshot Manager 的回應如下：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-165">When it connects to a device, StorSimple Snapshot Manager responds as follows:</span></span>
   
   * <span data-ttu-id="ecdcb-166">如果由於任何原因而無法使用裝置，StorSimple Snapshot Manager 會傳回錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-166">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> 
   
   * <span data-ttu-id="ecdcb-167">如果裝置可用，StorSimple Snapshot Manager 會新增連接。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-167">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="ecdcb-168">當您選取裝置時，它會出現在 [結果] 窗格中，而且狀態欄位會指出該裝置 [可用]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-168">When you select the device, it appears in the **Results** pane, and the status field indicates that the device is **Available**.</span></span> <span data-ttu-id="ecdcb-169">StorSimple Snapshot Manager 會匯入任何針對裝置設定的磁碟區群組，前提是磁碟區群組具有相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-169">StorSimple Snapshot Manager imports any volume groups configured for the device, provided that the volume groups have associated backups.</span></span> <span data-ttu-id="ecdcb-170">不會匯入備份原則。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-170">Backup policies are not imported.</span></span> <span data-ttu-id="ecdcb-171">不會匯入沒有相關聯之備份的磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-171">Volume groups that do not have associated backups are not imported.</span></span>
2. <span data-ttu-id="ecdcb-172">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-172">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
3. <span data-ttu-id="ecdcb-173">以滑鼠右鍵按一下 [範圍] 窗格中的最上層節點，然後按一下 [切換匯入顯示]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-173">Right-click the top node in the **Scope** pane, and then click **Toggle Imports Display**.</span></span>
   
    ![選取 [切換匯入顯示]](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. <span data-ttu-id="ecdcb-175">[ **切換匯入顯示** ] 對話方塊隨即出現，顯示已匯入之磁碟區群組和備份的狀態。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-175">The **Toggle Imports Display** dialog box appears, showing the status of the imported volume groups and backups.</span></span> <span data-ttu-id="ecdcb-176">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-176">Click **OK**.</span></span>

<span data-ttu-id="ecdcb-177">在順利匯入磁碟區群組和備份之後，您可以使用 StorSimple Snapshot Manager 來管理它們，就如同您管理您使用 StorSimple Snapshot Manager 所建立並設定的磁碟區群組和備份一般。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-177">After the volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager to manage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span></span> 

## <a name="refresh-connected-devices"></a><span data-ttu-id="ecdcb-178">重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-178">Refresh connected devices</span></span>
<span data-ttu-id="ecdcb-179">請使用下列程序，同步處理已連接的 StorSimple 裝置與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-179">Use the following procedure to synchronize the connected StorSimple devices with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-connected-devices"></a><span data-ttu-id="ecdcb-180">若要重新整理已連接的裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-180">To refresh connected devices</span></span>
1. <span data-ttu-id="ecdcb-181">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-181">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ecdcb-182">在 [範圍] 窗格中，以滑鼠右鍵按一下 [裝置]，然後按一下 [重新整理裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-182">In the **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span></span> <span data-ttu-id="ecdcb-183">這會同步處理已連接的裝置與 StorSimple Snapshot Manager，讓您可以檢視磁碟區群組和備份，包括任何最近新增的項目。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-183">This synchronizes the connected devices with StorSimple Snapshot Manager so that you can view the volume groups and backups, including any recent additions.</span></span> 
   
    ![重新整理 StorSimple 裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

<span data-ttu-id="ecdcb-185">[ **重新整理裝置** ] 動作會從已連接的裝置擷取任何新的磁碟區群組和任何相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-185">The **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span></span> <span data-ttu-id="ecdcb-186">不同於適用於 [磁碟區] 節點的 [重新掃描磁碟區] 動作，[重新整理裝置] 不會還原備份登錄。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-186">Unlike the **Rescan volumes** action available for the **Volumes** node, **Refresh Devices** does not restore the backup registry.</span></span>

## <a name="authenticate-a-device"></a><span data-ttu-id="ecdcb-187">驗證裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-187">Authenticate a device</span></span>
<span data-ttu-id="ecdcb-188">請使用下列程序，利用 StorSimple Snapshot Manager 來驗證 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-188">Use the following procedure to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-authenticate-a-device"></a><span data-ttu-id="ecdcb-189">若要驗證裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-189">To authenticate a device</span></span>
1. <span data-ttu-id="ecdcb-190">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-190">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ecdcb-191">在 [範圍] 窗格中，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-191">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="ecdcb-192">在 [結果] 窗格中，以滑鼠右鍵按一下裝置的名稱，然後按一下 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-192">In the **Results** pane, right-click the name of the device, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="ecdcb-193">[ **驗證** ] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-193">The **Authenticate** dialog box appears.</span></span> <span data-ttu-id="ecdcb-194">輸入裝置密碼，然後按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-194">Type the device password, and then click **OK**.</span></span>
   
    ![[驗證] 對話方塊](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a><span data-ttu-id="ecdcb-196">檢視裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="ecdcb-196">View device details</span></span>
<span data-ttu-id="ecdcb-197">請使用下列程序來檢視 StorSimple 裝置的詳細資料，如有必要，請重新同步處理裝置與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-197">Use the following procedure to view the details of a StorSimple device and, if necessary, resynchronize the device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-view-and-resynchronize-device-details"></a><span data-ttu-id="ecdcb-198">若要檢視和重新同步處理裝置詳細資料</span><span class="sxs-lookup"><span data-stu-id="ecdcb-198">To view and resynchronize device details</span></span>
1. <span data-ttu-id="ecdcb-199">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-199">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ecdcb-200">在 [範圍] 窗格中，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-200">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="ecdcb-201">在 [結果] 窗格中，以滑鼠右鍵按一下裝置的名稱，然後按一下 [詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-201">In the **Results** pane, right-click the name of the device, and then click **Details**.</span></span>

<span data-ttu-id="ecdcb-202">4. [裝置詳細資料] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-202">4.The **Device Details** dialog box appears.</span></span> <span data-ttu-id="ecdcb-203">此方塊會顯示名稱、型號、版本、序號、狀態、目標 iSCSI 合格名稱 (IQN)，以及上次同步處理日期和時間。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-203">This box shows the name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span></span>

* <span data-ttu-id="ecdcb-204">按一下 [ **重新同步處理** ] 以同步處理裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-204">Click **Resync** to synchronize the device.</span></span>
* <span data-ttu-id="ecdcb-205">按一下 [確定] 或 [取消] 以關閉對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-205">Click **OK** or **Cancel** to close the dialog box.</span></span>
  
  ![裝置詳細資料](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a><span data-ttu-id="ecdcb-207">重新整理個別裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-207">Refresh an individual device</span></span>
<span data-ttu-id="ecdcb-208">請使用下列程序，來重新同步處理個別的 StorSimple 裝置與 StorSimple Snapshot Manager 。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-208">Use the following procedure to resynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-a-device"></a><span data-ttu-id="ecdcb-209">若要重新整理裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-209">To refresh a device</span></span>
1. <span data-ttu-id="ecdcb-210">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-210">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="ecdcb-211">在 [範圍] 窗格中，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-211">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="ecdcb-212">在 [結果] 窗格中，以滑鼠右鍵按一下裝置的名稱，然後按一下 [重新整理裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-212">In the **Results** pane, right-click the name of the device, and then click **Refresh Device**.</span></span> <span data-ttu-id="ecdcb-213">這會同步處理裝置與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-213">This synchronizes the device with StorSimple Snapshot Manager.</span></span>

## <a name="delete-a-device-configuration"></a><span data-ttu-id="ecdcb-214">刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="ecdcb-214">Delete a device configuration</span></span>
<span data-ttu-id="ecdcb-215">請使用下列程序，從 StorSimple Snapshot Manager 刪除個別的 StorSimple 裝置組態。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-215">Use the following procedure to delete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span></span>

#### <a name="to-delete-a-device-configuration"></a><span data-ttu-id="ecdcb-216">若要刪除裝置組態</span><span class="sxs-lookup"><span data-stu-id="ecdcb-216">To delete a device configuration</span></span>
1. <span data-ttu-id="ecdcb-217">按一下桌面圖示，以啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-217">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ecdcb-218">在 [範圍] 窗格中，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-218">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="ecdcb-219">在 [結果] 窗格中，以滑鼠右鍵按一下裝置的名稱，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-219">In the **Results** pane, right-click the name of the device, and then click **Delete**.</span></span> 
4. <span data-ttu-id="ecdcb-220">下列訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-220">The following message appears.</span></span> <span data-ttu-id="ecdcb-221">按一下 [是] 以刪除組態，或按一下 [否] 以取消刪除。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-221">Click **Yes** to delete the configuration or click **No** to cancel the deletion.</span></span>
   
    ![刪除裝置組態](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a><span data-ttu-id="ecdcb-223">變更過期的裝置密碼</span><span class="sxs-lookup"><span data-stu-id="ecdcb-223">Change an expired device password</span></span>
<span data-ttu-id="ecdcb-224">您必須輸入密碼，才能使用 StorSimple Snapshot Manager 驗證 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-224">You must enter a password to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="ecdcb-225">當使用 Windows PowerShell 介面來設定裝置時，您可以設定此密碼。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-225">You configure this password when you use the Windows PowerShell interface to set up the device.</span></span> <span data-ttu-id="ecdcb-226">不過，密碼會過期。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-226">However, the password can expire.</span></span> <span data-ttu-id="ecdcb-227">如果發生這種情況，您可以使用 Azure 傳統入口網站變更密碼。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-227">If this happens, you can use the Azure classic portal to change the password.</span></span> <span data-ttu-id="ecdcb-228">然後，因為在密碼過期之前，已在 StorSimple Snapshot Manager 設定裝置，所以您必須在 StorSimple Snapshot Manager 重新驗證裝置。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-228">Then, because the device was configured in StorSimple Snapshot Manager before the password expired, you must re-authenticate the device in StorSimple Snapshot Manager.</span></span>

#### <a name="to-change-the-expired-password"></a><span data-ttu-id="ecdcb-229">若要變更過期的密碼</span><span class="sxs-lookup"><span data-stu-id="ecdcb-229">To change the expired password</span></span>
1. <span data-ttu-id="ecdcb-230">在 Azure 傳統入口網站中，啟動 StorSimple Manager 服務。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-230">In the Azure classic portal, start the StorSimple Manager service.</span></span>
2. <span data-ttu-id="ecdcb-231">按一下 確定 **裝置** > **設定** 。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-231">Click **Devices** > **Configure** for the device.</span></span>
3. <span data-ttu-id="ecdcb-232">向下捲動到 StorSimple Snapshot Manager 區段。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-232">Scroll down to the StorSimple Snapshot Manager section.</span></span> <span data-ttu-id="ecdcb-233">輸入 14 或 15 個字元的密碼。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-233">Enter a password that is 14-15 characters.</span></span> <span data-ttu-id="ecdcb-234">請確定密碼混有大寫、小寫、數字和特殊字元。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-234">Make sure that the password contains a mix of uppercase, lowercase, numeric, and special characters.</span></span>
4. <span data-ttu-id="ecdcb-235">請重新輸入密碼加以確認。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-235">Re-enter the password to confirm it.</span></span>
5. <span data-ttu-id="ecdcb-236">按一下頁面底部的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-236">Click **Save** at the bottom of the page.</span></span>

#### <a name="to-re-authenticate-the-device"></a><span data-ttu-id="ecdcb-237">若要重新驗證裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-237">To re-authenticate the device</span></span>
1. <span data-ttu-id="ecdcb-238">啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-238">Start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="ecdcb-239">在 [範圍] 窗格中，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-239">In the **Scope** pane, click **Devices**.</span></span> <span data-ttu-id="ecdcb-240">已設定的裝置清單會出現在 [ **結果** ] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-240">A list of configured devices appears in the **Results** pane.</span></span>
3. <span data-ttu-id="ecdcb-241">選取裝置、按一下滑鼠右鍵，然後按一下 [ **驗證**]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-241">Select the device, right-click, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="ecdcb-242">在 [ **驗證** ] 視窗中，輸入新密碼。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-242">In the **Authenticate** window, enter the new password.</span></span>
5. <span data-ttu-id="ecdcb-243">選取裝置、按一下滑鼠右鍵，然後選取 [ **重新整理裝置**]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-243">Select the device, right-click, and select **Refresh device**.</span></span> <span data-ttu-id="ecdcb-244">這會同步處理裝置與 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-244">This synchronizes the device with StorSimple Snapshot Manager.</span></span>

## <a name="replace-a-failed-device"></a><span data-ttu-id="ecdcb-245">更換故障的裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-245">Replace a failed device</span></span>
<span data-ttu-id="ecdcb-246">如果 StorSimple 裝置故障，並更換為備用 (容錯移轉) 裝置，請使用下列步驟，連接至新裝置並檢視相關聯的備份。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-246">If a StorSimple device fails and is replaced by a standby (failover) device, use the following steps to connect to the new device and view the associated backups.</span></span>

#### <a name="to-connect-to-a-new-device-after-failover"></a><span data-ttu-id="ecdcb-247">若要在容錯移轉之後連接至新裝置</span><span class="sxs-lookup"><span data-stu-id="ecdcb-247">To connect to a new device after failover</span></span>
1. <span data-ttu-id="ecdcb-248">重新設定新裝置的 iSCSI 連接。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-248">Reconfigure the iSCSI connection to the new device.</span></span> <span data-ttu-id="ecdcb-249">如需相關指示，請移至 [部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)中的「步驟 7：掛載、初始化和格式磁碟區」。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-249">For instructions, go to "Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ecdcb-250">如果新的 StorSimple 裝置具有與舊裝置相同的 IP 位址，則您也許能夠連接舊組態。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-250">If the new StorSimple device has the same IP address as the old one, you might be able to connect the old configuration.</span></span>


1. <span data-ttu-id="ecdcb-251">停止 Microsoft StorSimple 管理服務：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-251">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="ecdcb-252">啟動伺服器管理員。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-252">Start Server Manager.</span></span>
   2. <span data-ttu-id="ecdcb-253">在伺服器管理員儀表板的 [工具] 功能表上，選取 [服務]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-253">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   3. <span data-ttu-id="ecdcb-254">在 [服務] 視窗中，選取 [Microsoft StorSimple 管理服務]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-254">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span>
   4. <span data-ttu-id="ecdcb-255">在右窗格的 [Microsoft StorSimple 管理服務] 之下，按一下 [停止服務]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-255">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span>
2. <span data-ttu-id="ecdcb-256">移除與舊裝置相關的組態資訊：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-256">Remove the configuration information related to the old device:</span></span>
   
   1. <span data-ttu-id="ecdcb-257">在 [檔案總管] 中，瀏覽至 C:\ProgramData\Microsoft\StorSimple\BACatalog.</span><span class="sxs-lookup"><span data-stu-id="ecdcb-257">In File Explorer, browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span>
   2. <span data-ttu-id="ecdcb-258">刪除 BACatalog 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-258">Delete the files in the BACatalog folder.</span></span>
3. <span data-ttu-id="ecdcb-259">重新啟動 Microsoft StorSimple 管理服務：</span><span class="sxs-lookup"><span data-stu-id="ecdcb-259">Restart the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="ecdcb-260">在伺服器管理員儀表板的 [工具] 功能表上，選取 [服務]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-260">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span>
   2. <span data-ttu-id="ecdcb-261">在 [服務] 視窗中，選取 [Microsoft StorSimple 管理服務]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-261">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span>
   3. <span data-ttu-id="ecdcb-262">在右窗格的 [Microsoft StorSimple 管理服務] 之下，按一下 [重新啟動服務]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-262">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span>
4. <span data-ttu-id="ecdcb-263">啟動 StorSimple Snapshot Manager。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-263">Start StorSimple Snapshot Manager.</span></span>
5. <span data-ttu-id="ecdcb-264">若要設定新的 StorSimple 裝置，請完成＜部署 StorSimple Snapshot Manager＞中的 [步驟 2：連接 StorSimple 裝置](storsimple-snapshot-manager-deployment.md)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-264">To configure the new StorSimple device, complete the steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span>
6. <span data-ttu-id="ecdcb-265">以滑鼠右鍵按一下 [範圍] 窗格中的最上層節點 (範例中的 StorSimple Snapshot Manager)，然後按一下 [切換匯入顯示]。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-265">Right-click the top-level node in the **Scope** pane (StorSimple Snapshot Manager in the example), and then click **Toggle Imports Display**.</span></span> 
7. <span data-ttu-id="ecdcb-266">當可在 StorSimple Snapshot Manager 中看到匯入的磁碟區群組和備份時，即會出現一則訊息。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-266">A message appears when the imported volume groups and backups are visible in StorSimple Snapshot Manager.</span></span> <span data-ttu-id="ecdcb-267">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-267">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecdcb-268">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecdcb-268">Next steps</span></span>
* <span data-ttu-id="ecdcb-269">了解如何 [使用 StorSimple Snapshot Manager 來管理您的 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-269">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="ecdcb-270">了解如何 [使用 StorSimple Snapshot Manager 來檢視和管理磁碟區](storsimple-snapshot-manager-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="ecdcb-270">Learn how to [use StorSimple Snapshot Manager to view and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span></span>

