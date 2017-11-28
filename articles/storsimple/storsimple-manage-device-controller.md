---
title: "管理 StorSimple 裝置控制器 | Microsoft Docs"
description: "了解如何停止、重新啟動、關閉或重設您的 StorSimple 裝置控制器。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 67dbb0c4066002256efbab6061157c641527e441
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-storsimple-device-controllers"></a><span data-ttu-id="e2bf5-103">管理 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="e2bf5-103">Manage your StorSimple device controllers</span></span>
## <a name="overview"></a><span data-ttu-id="e2bf5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e2bf5-104">Overview</span></span>
<span data-ttu-id="e2bf5-105">本教學課程描述可在 StorSimple 裝置控制器上執行的不同作業。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-105">This tutorial describes the different operations that can be performed on your StorSimple device controllers.</span></span> <span data-ttu-id="e2bf5-106">StorSimple 裝置中的控制器在主動-被動組態中是備援 (對等) 控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-106">The controllers in your StorSimple device are redundant (peer) controllers in an active-passive configuration.</span></span> <span data-ttu-id="e2bf5-107">在指定的時間中，只能有一個控制器在主動模式，並處理所有磁碟和網路作業。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-107">At a given time, only one controller is active and is processing all the disk and network operations.</span></span> <span data-ttu-id="e2bf5-108">另一個控制器處於被動模式。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-108">The other controller is in a passive mode.</span></span> <span data-ttu-id="e2bf5-109">如果主動控制器發生故障，被動控制器便會自動變為主動。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-109">If the active controller fails, the passive controller becomes active automatically.</span></span>

<span data-ttu-id="e2bf5-110">本教學課程包含使用下列內容管理裝置控制器的逐步指示：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-110">This tutorial includes step-by-step instructions to manage the device controllers by using the:</span></span>

* <span data-ttu-id="e2bf5-111">StorSimple Manager 服務中 [維護] 頁面的 [控制器] 區段</span><span class="sxs-lookup"><span data-stu-id="e2bf5-111">**Controllers** section of the **Maintenance** page in the StorSimple Manager service</span></span>
* <span data-ttu-id="e2bf5-112">Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="e2bf5-112">Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="e2bf5-113">我們建議您透過 StorSimple Manager 服務管理裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-113">We recommend that you manage the device controllers via the StorSimple Manager service.</span></span> <span data-ttu-id="e2bf5-114">如果動作只能使用 Windows PowerShell for StorSimple 執行，本教學課程會記錄下來。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-114">If an action can only be performed by using Windows PowerShell for StorSimple, the tutorial makes a note of it.</span></span>

<span data-ttu-id="e2bf5-115">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-115">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="e2bf5-116">重新啟動或關閉 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="e2bf5-116">Restart or shut down a StorSimple device controller</span></span>
* <span data-ttu-id="e2bf5-117">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="e2bf5-117">Shut down a StorSimple device</span></span>
* <span data-ttu-id="e2bf5-118">將 StorSimple 裝置重設為原廠預設值</span><span class="sxs-lookup"><span data-stu-id="e2bf5-118">Reset your StorSimple device to factory defaults</span></span>

## <a name="restart-or-shut-down-a-single-controller"></a><span data-ttu-id="e2bf5-119">重新啟動或關閉單一控制器</span><span class="sxs-lookup"><span data-stu-id="e2bf5-119">Restart or shut down a single controller</span></span>
<span data-ttu-id="e2bf5-120">一般系統作業並不需要重新啟動或關閉控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-120">A controller restart or shutdown is not required as a part of normal system operation.</span></span> <span data-ttu-id="e2bf5-121">只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-121">Shutdown operations for a single device controller are common only in cases in which a failed device hardware component requires replacement.</span></span> <span data-ttu-id="e2bf5-122">只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-122">A controller restart may also be required in a situation in which performance is affected by excessive memory usage or a malfunctioning controller.</span></span> <span data-ttu-id="e2bf5-123">成功更換控制器之後，如果您想要啟用並測試更換的控制器，也可能需要重新啟動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-123">You may also need to restart a controller after a successful controller replacement, if you wish to enable and test the replaced controller.</span></span>

<span data-ttu-id="e2bf5-124">假設被動控制器可用，重新啟動裝置並不會干擾連線的啟動器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-124">Restarting a device is not disruptive to connected initiators, assuming the passive controller is available.</span></span> <span data-ttu-id="e2bf5-125">如果被動控制器不可用或已關閉，重新啟動主動控制器可能會導致服務中斷和停機。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-125">If a passive controller is not available or turned off, then restarting the active controller may result in the disruption of service and downtime.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="e2bf5-126">**執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-126">**A running controller should never be physically removed as this would result in a loss of redundancy and an increased risk of downtime.**</span></span>
> * <span data-ttu-id="e2bf5-127">下列程序只適用於 StorSimple 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-127">The following procedure applies only to the StorSimple physical device.</span></span> <span data-ttu-id="e2bf5-128">如需有關如何啟動、停止和重新啟動虛擬裝置的資訊，請參閱[使用虛擬裝置](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-128">For information about how to start, stop, and restart the virtual device, see [Work with the virtual device](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).</span></span>
> 
> 

<span data-ttu-id="e2bf5-129">您可以使用 StorSimple Manager 服務或 Windows PowerShell for StorSimple 的 Azure 傳統入口網站重新啟動或關閉單一裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-129">You can restart or shut down a single device controller by using the Azure classic portal of the StorSimple Manager service or Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="e2bf5-130">若要從 Azure 傳統入口網站管理您的裝置控制器，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-130">To manage your device controllers from the Azure classic portal, perform the following steps.</span></span>

#### <a name="to-restart-or-shut-down-a-controller-in-classic-portal"></a><span data-ttu-id="e2bf5-131">若要在傳統入口網站中重新啟動或關閉控制器</span><span class="sxs-lookup"><span data-stu-id="e2bf5-131">To restart or shut down a controller in classic portal</span></span>
1. <span data-ttu-id="e2bf5-132">請瀏覽至 [裝置] > [維護]。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-132">Navigate to **Devices > Maintenance**.</span></span>
2. <span data-ttu-id="e2bf5-133">移至 [硬體狀態] 並確認裝置上的兩個控制器狀態為 [狀況良好]。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-133">Go to **Hardware Status** and verify that the status of both the controllers on your device is **Healthy**.</span></span>
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-manage-device-controller/IC766017.png)
3. <span data-ttu-id="e2bf5-135">在 [維護] 頁面的底部，按一下 [管理控制器]。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-135">From the bottom of the **Maintenance** page, click **Manage Controllers**.</span></span>
   
    ![管理 StorSimple 裝置控制器](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > <span data-ttu-id="e2bf5-137">如果您沒看到 [ **管理控制器**]，表示您需要安裝更新。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-137">If you cannot see **Manage Controllers**, then you need to install updates.</span></span> <span data-ttu-id="e2bf5-138">如需詳細資訊，請參閱 [更新您的 StorSimple 裝置](storsimple-update-device.md)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-138">For more information, see [Update your StorSimple device](storsimple-update-device.md).</span></span>
   > 
   > 
4. <span data-ttu-id="e2bf5-139">在 [ **變更控制器設定** ] 對話方塊中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-139">In the **Change Controller Settings** dialog box, do the following:</span></span>
   
   1. <span data-ttu-id="e2bf5-140">從 [ **選取控制器** ] 下拉式清單中，選取您想要管理的控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-140">From the **Select Controller** drop-down list, select the controller that you want to manage.</span></span> <span data-ttu-id="e2bf5-141">選項為控制器 0 和控制器 1。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-141">The options are Controller 0 and Controller 1.</span></span> <span data-ttu-id="e2bf5-142">這些控制器也可識別為主動或被動。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-142">These controllers are also identified as active or passive.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e2bf5-143">如果控制器無法使用或已關閉，就無法管理它，而它也不會出現在下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-143">A controller cannot be managed if it is unavailable or turned off, and it will not appear in the drop-down list.</span></span>
      > 
      > 
   2. <span data-ttu-id="e2bf5-144">從 [選取動作] 下拉式清單中，選擇 [重新啟動控制器] 或 [關閉控制器]。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-144">From the **Select Action** drop-down list, choose **Restart controller** or **Shut down controller**.</span></span>
      
       ![重新啟動 StorSimple 裝置被動控制器](./media/storsimple-manage-device-controller/IC766020.png)
   3. <span data-ttu-id="e2bf5-146">按一下核取圖示 </span><span class="sxs-lookup"><span data-stu-id="e2bf5-146">Click the check icon</span></span> ![核取圖示](./media/storsimple-manage-device-controller/IC740895.png)<span data-ttu-id="e2bf5-148">。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-148">.</span></span>

<span data-ttu-id="e2bf5-149">這將會重新啟動或關閉控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-149">This will restart or shut down the controller.</span></span> <span data-ttu-id="e2bf5-150">下表根據您在 [ **變更控制器設定** ] 對話方塊中選取的項目，整理出所發生狀況的詳細資料摘要。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-150">The table below summarizes the details of what happens depending on the selections you have made in the **Change Controller Settings** dialog box.</span></span>  

| <span data-ttu-id="e2bf5-151">選取項目 #</span><span class="sxs-lookup"><span data-stu-id="e2bf5-151">Selection #</span></span> | <span data-ttu-id="e2bf5-152">如果您選擇...</span><span class="sxs-lookup"><span data-stu-id="e2bf5-152">If you choose to...</span></span> | <span data-ttu-id="e2bf5-153">就會發生這個狀況。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-153">This will happen.</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2bf5-154">1.</span><span class="sxs-lookup"><span data-stu-id="e2bf5-154">1.</span></span> |<span data-ttu-id="e2bf5-155">重新啟動被動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-155">Restart the passive controller.</span></span> |<span data-ttu-id="e2bf5-156">會建立工作以重新啟動控制器，且您會在工作成功建立之後收到通知。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-156">A job will be created to restart the controller, and you will be notified after the job is successfully created.</span></span> <span data-ttu-id="e2bf5-157">這樣會起始控制器重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-157">This will initiate the controller restart.</span></span> <span data-ttu-id="e2bf5-158">依序存取[服務] > [儀表板] > [檢視作業記錄檔]，然後根據您服務的特定參數進行篩選，您就能監視重新啟動程序。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-158">You can monitor the restart process by accessing **Service > Dashboard > View operation logs** and then filtering by parameters specific to your service.</span></span> |
| <span data-ttu-id="e2bf5-159">2.</span><span class="sxs-lookup"><span data-stu-id="e2bf5-159">2.</span></span> |<span data-ttu-id="e2bf5-160">重新啟動主動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-160">Restart the active controller.</span></span> |<span data-ttu-id="e2bf5-161">您會看到下列警告：「如果您重新啟動主動控制器，裝置將容錯移轉到被動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-161">You will see the following warning: "If you restart the active controller, the device will fail over to the passive controller.</span></span> <span data-ttu-id="e2bf5-162">您要繼續嗎？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-162">Do you want to continue?"</span></span> </br><span data-ttu-id="e2bf5-163">如果您選擇繼續進行這項作業，接下來的步驟與重新啟動被動控制器的步驟相同 (請參閱選取項目 1)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-163">If you choose to proceed with this operation, the next steps will be identical to those used to restart the passive controller (see selection 1).</span></span> |
| <span data-ttu-id="e2bf5-164">3.</span><span class="sxs-lookup"><span data-stu-id="e2bf5-164">3.</span></span> |<span data-ttu-id="e2bf5-165">關閉被動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-165">Shut down the passive controller.</span></span> |<span data-ttu-id="e2bf5-166">您會看到下列訊息：「關閉完成之後，您必須按下控制器上的電源按鈕以將其開啟。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-166">You will see the following message: "After shutdown is complete, you will need to push the power button on your controller to turn it on.</span></span> <span data-ttu-id="e2bf5-167">您確定要關閉此控制器嗎？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-167">Are you sure you want to shut down this controller?"</span></span> </br><span data-ttu-id="e2bf5-168">如果您選擇繼續進行這項作業，接下來的步驟與重新啟動被動控制器的步驟相同 (請參閱選取項目 1)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-168">If you choose to proceed with this operation, the next steps will be identical to those used to restart the passive controller (see selection 1).</span></span> |
| <span data-ttu-id="e2bf5-169">4.</span><span class="sxs-lookup"><span data-stu-id="e2bf5-169">4.</span></span> |<span data-ttu-id="e2bf5-170">關閉主動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-170">Shut down the active controller.</span></span> |<span data-ttu-id="e2bf5-171">您會看到下列訊息：「關閉完成之後，您必須按下控制器上的電源按鈕以將其開啟。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-171">You will see the following message: "After shutdown is complete, you will need to push the power button on your controller to turn it on.</span></span> <span data-ttu-id="e2bf5-172">您確定要關閉此控制器嗎？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-172">Are you sure you want to shut down this controller?"</span></span> </br><span data-ttu-id="e2bf5-173">如果您選擇繼續進行這項作業，接下來的步驟與重新啟動被動控制器的步驟相同 (請參閱選取項目 1)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-173">If you choose to proceed with this operation, the next steps will be identical to those used to restart the passive controller (see selection 1).</span></span> |

#### <a name="to-restart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a><span data-ttu-id="e2bf5-174">重新啟動或關閉 Windows PowerShell for StorSimple 中的控制器</span><span class="sxs-lookup"><span data-stu-id="e2bf5-174">To restart or shut down a controller in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="e2bf5-175">執行下列步驟以從 Azure 傳統入口網站關閉或重新啟動 StorSimple 裝置上的單一控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-175">Perform the following steps to shut down or restart a single controller on your StorSimple device from the Azure classic portal.</span></span>

1. <span data-ttu-id="e2bf5-176">使用序列主控台或 telnet 工作階段，從遠端電腦存取裝置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-176">Access the device by using the serial console or a telnet session from a remote computer.</span></span> <span data-ttu-id="e2bf5-177">遵循 [使用 PuTTY 連接到裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的步驟，連接到控制器 0 或控制器 1。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-177">Connect to Controller 0 or Controller 1 by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="e2bf5-178">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-178">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="e2bf5-179">在橫幅訊息中，記下您已連接的控制器 (控制器 0 或控制器 1) 以及它是主動或被動 (待命) 控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-179">In the banner message, make a note of the controller you are connected to (Controller 0 or Controller 1) and whether it is the active or the passive (standby) controller.</span></span>
   
   * <span data-ttu-id="e2bf5-180">若要關閉單一控制器，請在提示中輸入：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-180">To shut down a single controller, at the prompt, type:</span></span>
     
       `Stop-HcsController`
     
       <span data-ttu-id="e2bf5-181">這會關閉您所連接的控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-181">This will shut down the controller that you are connected to.</span></span> <span data-ttu-id="e2bf5-182">如果您停止主動控制器，它會在關閉之前容錯移轉到被動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-182">If you stop the active controller, then it will fail over to the passive controller before it shuts down.</span></span>
   * <span data-ttu-id="e2bf5-183">若要重新啟動控制器，請在提示中輸入：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-183">To restart a controller, at the prompt, type:</span></span>
     
       `Restart-HcsController`
     
       <span data-ttu-id="e2bf5-184">這會重新啟動您所連接的控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-184">This will restart the controller that you are connected to.</span></span> <span data-ttu-id="e2bf5-185">如果您重新啟動主動控制器，它會在重新啟動之前容錯移轉到主動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-185">If you restart the active controller, it will fail over to the passive controller before the restart.</span></span>

## <a name="shut-down-a-storsimple-device"></a><span data-ttu-id="e2bf5-186">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="e2bf5-186">Shut down a StorSimple device</span></span>
<span data-ttu-id="e2bf5-187">本節說明如何從遠端電腦關閉執行中或失敗的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-187">This section explains how to shut down a running or a failed StorSimple device from a remote computer.</span></span> <span data-ttu-id="e2bf5-188">裝置會在關閉兩個裝置控制器之後關閉。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-188">A device is turned off after shutting down both the device controllers.</span></span> <span data-ttu-id="e2bf5-189">當裝置正在實際移動，或被帶離服務時，則已經完成裝置關閉。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-189">A device shutdown is done when the device is being physically moved, or is taken out of service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2bf5-190">關閉裝置之前，請檢查裝置元件的健全狀態。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-190">Before you shut down the device, check the health of the device components.</span></span> <span data-ttu-id="e2bf5-191">瀏覽至 [裝置] > [維護] > [硬體狀態] 並確認所有元件的 LED 燈狀態為綠色。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-191">Navigate to **Devices > Maintenance > Hardware Status** and verify that the LED status of all the components is green.</span></span> <span data-ttu-id="e2bf5-192">只有狀況良好的裝置才會有綠色的狀態。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-192">Only a healthy device will have a green status.</span></span> <span data-ttu-id="e2bf5-193">如果您的裝置正在關閉以更換故障的元件，您會看到個別元件的失敗 (紅色) 或降級 (黃色) 狀態。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-193">If your device is being shut down to replace a malfunctioning component, you will see a failed (red) or a degraded (yellow) status for the respective component(s).</span></span>
> 
> 

#### <a name="to-shut-down-a-storsimple-device"></a><span data-ttu-id="e2bf5-194">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="e2bf5-194">To shut down a StorSimple device</span></span>
1. <span data-ttu-id="e2bf5-195">透過 [重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller) 程序，識別和關閉裝置上的被動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-195">Use the [restart or shut down a controller](#restart-or-shut-down-a-single-controller) procedure to identify and shut down the passive controller on your device.</span></span> <span data-ttu-id="e2bf5-196">您可以在 Azure 傳統入口網站或 Windows PowerShell for StorSimple 中執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-196">You can perform this operation in the Azure classic portal or in Windows PowerShell for StorSimple.</span></span>
2. <span data-ttu-id="e2bf5-197">重複上述步驟來關閉主動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-197">Repeat the above step to shut down the active controller.</span></span>
3. <span data-ttu-id="e2bf5-198">您現在必須查看裝置的背板。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-198">You will now need to look at the back plane of the device.</span></span> <span data-ttu-id="e2bf5-199">完全關閉兩個控制器之後，兩個控制器上的狀態 Led 應該為閃爍的紅色。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-199">After the two controllers are completely shut down, the status LEDs on both the controllers should be blinking red.</span></span> <span data-ttu-id="e2bf5-200">如果您需要在此時將裝置完全關閉，請將電源和冷卻模組 (PCM) 上的電源開關切換為 OFF 的位置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-200">If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.</span></span> <span data-ttu-id="e2bf5-201">這樣可以關閉裝置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-201">This should turn off the device.</span></span>

<!--#### To shut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect to the serial console of the StorSimple device by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In the serial console menu, verify from the banner message that the controller you are connected to is the passive controller. If you are connected to the active controller, disconnect from this controller and connect to the other controller.

1. In the serial console menu, choose option 1, **log in with full access**.

1. At the prompt, type:

    `Stop-HCSController`

    This should shut down the current controller. To verify whether the shutdown has finished, check the back of the device. The controller status LED should be solid red.

1. Repeat steps 1 through 4 to connect to the active controller and then shut it down.

1. After both the controllers are completely shut down, the status LEDs on both should be blinking red. If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.-->

## <a name="reset-the-device-to-factory-default-settings"></a><span data-ttu-id="e2bf5-202">將裝置重設為出廠預設設定。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-202">Reset the device to factory default settings</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e2bf5-203">如果您需要將裝置重設為原廠預設設定，請聯絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-203">If you need to reset your device to factory default settings, contact Microsoft Support.</span></span> <span data-ttu-id="e2bf5-204">以下所述的程序，應只用於搭配 Microsoft 支援服務時使用。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-204">The procedure described below should be used only in conjunction with Microsoft Support.</span></span>
> 
> 

<span data-ttu-id="e2bf5-205">此程序描述如何將 Microsoft Azure StorSimple 裝置重設為使用 Windows PowerShell for StorSimple 的出廠預設設定。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-205">This procedure describes how to reset your Microsoft Azure StorSimple device to factory default settings using Windows PowerShell for StorSimple.</span></span>
<span data-ttu-id="e2bf5-206">根據預設，重設裝置會從整個叢集移除所有資料和設定。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-206">Resetting a device removes all data and settings from the entire cluster by default.</span></span>

<span data-ttu-id="e2bf5-207">執行下列步驟來將 Microsoft Azure StorSimple 裝置重設為出廠預設設定：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-207">Perform the following steps to reset your Microsoft Azure StorSimple device to factory default settings:</span></span>

### <a name="to-reset-the-device-to-default-settings-in-windows-powershell-for-storsimple"></a><span data-ttu-id="e2bf5-208">將裝置重設為 Windows PowerShell for StorSimple 中的預設設定</span><span class="sxs-lookup"><span data-stu-id="e2bf5-208">To reset the device to default settings in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="e2bf5-209">透過裝置的序列主控台存取裝置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-209">Access the device through its serial console.</span></span> <span data-ttu-id="e2bf5-210">檢查橫幅訊息以確保您已連接到主動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-210">Check the banner message to ensure that you are connected to the Active controller.</span></span>
2. <span data-ttu-id="e2bf5-211">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-211">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="e2bf5-212">在提示中，輸入下列命令來重設整個叢集，移除所有資料、中繼資料和控制器設定︰</span><span class="sxs-lookup"><span data-stu-id="e2bf5-212">At the prompt, type the following command to reset the entire cluster, removing all data, metadata, and controller settings:</span></span>
   
    `Reset-HcsFactoryDefault`
   
    <span data-ttu-id="e2bf5-213">若要改為重設單一控制站，請使用 [Reset-HcsFactoryDefault`-scope` Cmdlet 搭配 ](http://technet.microsoft.com/library/dn688132.aspx) 參數。)</span><span class="sxs-lookup"><span data-stu-id="e2bf5-213">To instead reset a single controller, use the  [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet with the `-scope` parameter.)</span></span>
   
    <span data-ttu-id="e2bf5-214">系統會重新啟動多次。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-214">The system will reboot multiple times.</span></span> <span data-ttu-id="e2bf5-215">重設成功完成時，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-215">You will be notified when the reset has successfully completed.</span></span> <span data-ttu-id="e2bf5-216">根據系統模型，8100 裝置可能需要 45-60 分鐘來完成此程序，而 8600 需要 60-90 分鐘。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-216">Depending on the system model, it can take 45-60 minutes for an 8100 device and 60-90 minutes for an 8600 to finish this process.</span></span>
   
   > [!TIP]
   > * <span data-ttu-id="e2bf5-217">如果您使用 Update 1.2 或更早版本，請使用 `–SkipFirmwareVersionCheck` 參數略過韌體版本檢查 (否則您將看到韌體不符錯誤：恢復出廠預設值因韌體版本不相符而無法繼續。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-217">If you're using Update 1.2 or earlier use the `–SkipFirmwareVersionCheck` parameter to skip the firmware version check (otherwise you'll see a firmware mismatch error: Factory reset cannot continue due to a mismatch in the firmware versions.</span></span> <span data-ttu-id="e2bf5-218">)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-218">).</span></span>
   > * <span data-ttu-id="e2bf5-219">在 Government 入口網站中執行 Update 1 或 1.1 ，且已執行成功的單一或雙重控制器更換 (含 pre-Update 1 軟體所隨附的更換控制器) 的 StorSimple 裝置的恢復出廠預設值程序可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-219">The factory reset procedure may fail for StorSimple devices that are running Update 1 or 1.1 in the Government portal and have performed a successful single or dual controller replacement (with replacement controllers that were shipped with pre-Update 1 software).</span></span> <span data-ttu-id="e2bf5-220">這會發生在針對不存在於 pre-Update 1 軟體的控制器上的 SHA1 檔案的目前狀態驗證恢復出廠預設值時。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-220">This happens when the factory reset image is validated for the presence of a SHA1 file on the controller that does not exist for pre-Update 1 software.</span></span> <span data-ttu-id="e2bf5-221">如果您看到這個恢復出廠預設值失敗，請連絡 Microsoft 支援服務以協助您進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-221">If you see this factory reset failure, contact Microsoft Support to assist you with the next steps.</span></span> <span data-ttu-id="e2bf5-222">在具有 Update 1 或更新版本軟體的原廠出貨更換控制器不會看到這個問題。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-222">This issue is not seen with replacement controllers that were shipped from the factory with Update 1 or later software.</span></span>
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a><span data-ttu-id="e2bf5-223">有關管理裝置控制器的問題與解答</span><span class="sxs-lookup"><span data-stu-id="e2bf5-223">Questions and answers about managing device controllers</span></span>
<span data-ttu-id="e2bf5-224">在本節中，我們摘要說明一些有關管理 StorSimple 裝置控制器的常見問題。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-224">In this section, we have summarized some of the frequently asked questions regarding managing StorSimple device controllers.</span></span>

<span data-ttu-id="e2bf5-225">**問：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-225">**Q.**</span></span> <span data-ttu-id="e2bf5-226">如果裝置上的兩個控制器都狀況良好且已開啟，而我重新啟動或關閉主動控制器，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-226">What happens if both the controllers on my device are healthy and turned on and I restart or shut down the active controller?</span></span>

<span data-ttu-id="e2bf5-227">**答：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-227">**A.**</span></span> <span data-ttu-id="e2bf5-228">如果裝置上的兩個控制器皆狀況良好且已開啟，您會收到確認提示。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-228">If both the controllers on your device are healthy and turned on, you will be prompted for confirmation.</span></span> <span data-ttu-id="e2bf5-229">您可以選擇：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-229">You may choose to:</span></span>

* <span data-ttu-id="e2bf5-230">**重新啟動主動控制器** – 您會收到通知，告知您重新啟動主動控制器將使裝置容錯移轉到被動控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-230">**Restart the active controller** – You will be notified that restarting an active controller will cause the device to fail over to the passive controller.</span></span> <span data-ttu-id="e2bf5-231">控制器將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-231">The controller will restart.</span></span>
* <span data-ttu-id="e2bf5-232">**關閉主動控制器** – 您將會收到通知，告知您關閉主動控制器將導致停機。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-232">**Shut down an active controller** – You will be notified that shutting down an active controller will result in downtime.</span></span> <span data-ttu-id="e2bf5-233">您也必須在按下裝置上的電源按鈕以開啟控制器。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-233">You will also need to push the power button on the device to turn on the controller.</span></span>

<span data-ttu-id="e2bf5-234">**問：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-234">**Q.**</span></span> <span data-ttu-id="e2bf5-235">如果裝置上的被動控制器無法使用或已關閉，而我重新啟動或關閉主動控制器，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-235">What happens if the passive controller on my device is unavailable or turned off and I restart or shut down the active controller?</span></span>

<span data-ttu-id="e2bf5-236">**答：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-236">**A.**</span></span> <span data-ttu-id="e2bf5-237">如果裝置上的被動控制器無法使用或已關閉，而您選擇：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-237">If the passive controller on your device is unavailable or turned off, and you choose to:</span></span>

* <span data-ttu-id="e2bf5-238">**重新啟動主動控制器** – 您會收到通知，告知您繼續執行作業會導致服務暫時中斷，且您會收到確認提示。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-238">**Restart the active controller** – You will be notified that continuing the operation will result in a temporary disruption of the service, and you will be prompted for confirmation.</span></span>
* <span data-ttu-id="e2bf5-239">**關閉主動控制器** – 您會收到通知，告知您繼續執行作業會導致停機，而且您必須按下一或兩個控制器上的電源按鈕來開啟裝置。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-239">**Shut down an active controller** – You will be notified that continuing the operation will result in downtime, and that you will need to push the power button on one or both controllers to turn on the device.</span></span> <span data-ttu-id="e2bf5-240">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-240">You will be prompted for confirmation.</span></span>

<span data-ttu-id="e2bf5-241">**問：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-241">**Q.**</span></span> <span data-ttu-id="e2bf5-242">何時控制器重新啟動或關機會無法進行？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-242">When does the controller restart or shutdown fails to progress?</span></span>

<span data-ttu-id="e2bf5-243">**答：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-243">**A.**</span></span> <span data-ttu-id="e2bf5-244">重新啟動或關閉控制器可能會在下列情況下失敗：</span><span class="sxs-lookup"><span data-stu-id="e2bf5-244">Restarting or shutting down a controller may fail if:</span></span>

* <span data-ttu-id="e2bf5-245">裝置更新進行中。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-245">A device update is in progress.</span></span>
* <span data-ttu-id="e2bf5-246">控制器重新啟動已在進行中。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-246">A controller restart is already in progress.</span></span>
* <span data-ttu-id="e2bf5-247">控制器關閉已在進行中。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-247">A controller shutdown is already in progress.</span></span>

<span data-ttu-id="e2bf5-248">**問：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-248">**Q.**</span></span> <span data-ttu-id="e2bf5-249">您如何判斷控制器已重新啟動或關閉？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-249">How can you figure out if a controller was restarted or shut down?</span></span>

<span data-ttu-id="e2bf5-250">**答：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-250">**A.**</span></span> <span data-ttu-id="e2bf5-251">您可以檢查 [維護] 頁面上的控制器狀態。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-251">You can check the controller status on the Maintenance page.</span></span> <span data-ttu-id="e2bf5-252">控制器狀態會指出控制器已重新啟動或關閉。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-252">The controller status will indicate whether a controller has been restarted or shut down.</span></span> <span data-ttu-id="e2bf5-253">此外，如果控制器已重新啟動或關閉，[警示] 頁面會包含資訊警示。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-253">Additionally, the Alerts page will contain an informational alert if the controller was restarted or shut down.</span></span> <span data-ttu-id="e2bf5-254">控制器重新啟動和關閉作業也會記錄在作業記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-254">The controller restart and shutdown operations are also recorded in the operation logs.</span></span> <span data-ttu-id="e2bf5-255">如需有關作業記錄檔的詳細資訊，請移至 [檢視作業記錄檔](storsimple-service-dashboard.md#view-the-operations-logs)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-255">For more information about operation logs, go to [View the operation logs](storsimple-service-dashboard.md#view-the-operations-logs).</span></span>

<span data-ttu-id="e2bf5-256">**問：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-256">**Q.**</span></span> <span data-ttu-id="e2bf5-257">控制器容錯移轉會不會對 I/O 造成任何影響？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-257">Is there any impact to the I/Os as a result of controller failover?</span></span>

<span data-ttu-id="e2bf5-258">**答：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-258">**A.**</span></span> <span data-ttu-id="e2bf5-259">啟動器和主動控制器之間的 TCP 連接將會因為控制器容錯移轉而重設，但會在被動控制器繼續作業時重新建立。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-259">The TCP connections between initiators and active controller will be reset as a result of controller failover, but will be reestablished when the passive controller assumes operation.</span></span> <span data-ttu-id="e2bf5-260">在這項作業的過程中，啟動器與裝置之間的 I/O 活動中可能會有暫時的 (少於 30 秒) 暫停。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-260">There may be a temporary (less than 30 seconds) pause in I/O activity between initiators and the device during the course of this operation.</span></span>

<span data-ttu-id="e2bf5-261">**問：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-261">**Q.**</span></span> <span data-ttu-id="e2bf5-262">如何在控制器關閉並遭移除後，將控制器傳回給服務？</span><span class="sxs-lookup"><span data-stu-id="e2bf5-262">How do I return my controller to service after it has been shut down and removed?</span></span>

<span data-ttu-id="e2bf5-263">**答：**</span><span class="sxs-lookup"><span data-stu-id="e2bf5-263">**A.**</span></span> <span data-ttu-id="e2bf5-264">若要將控制器傳回給服務，您必須依照 [更換 StorSimple 裝置上的控制器模組](storsimple-controller-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-264">To return a controller to service, you must insert it into the chassis as described in [Replace a controller module on your StorSimple device](storsimple-controller-replacement.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2bf5-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2bf5-265">Next steps</span></span>
* <span data-ttu-id="e2bf5-266">如果發生任何無法使用本教學課程中所列之程序解決的 StorSimple 裝置控制器相關問題，請 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-266">If you encounter any issues with your StorSimple device controllers that you cannot resolve by using the procedures listed in this tutorial, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="e2bf5-267">若要深入了解使用 StorSimple Manager 的方式，請移至 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="e2bf5-267">To learn more about using the StorSimple Manager service, go to [Use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

