---
title: "管理 StorSimple 8000 系列裝置控制器 | Microsoft Docs"
description: "了解如何停止、重新啟動、關閉或重設您的 StorSimple 裝置控制器。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/19/2017
ms.author: alkohli
ms.openlocfilehash: 75c1bdb570967b6d1902697597f0b5bf3f4ffb7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-storsimple-device-controllers"></a><span data-ttu-id="70fcd-103">管理 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="70fcd-103">Manage your StorSimple device controllers</span></span>

## <a name="overview"></a><span data-ttu-id="70fcd-104">Overview</span><span class="sxs-lookup"><span data-stu-id="70fcd-104">Overview</span></span>

<span data-ttu-id="70fcd-105">本教學課程描述可在 StorSimple 裝置控制器上執行的不同作業。</span><span class="sxs-lookup"><span data-stu-id="70fcd-105">This tutorial describes the different operations that can be performed on your StorSimple device controllers.</span></span> <span data-ttu-id="70fcd-106">StorSimple 裝置中的控制器在主動-被動組態中是備援 (對等) 控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-106">The controllers in your StorSimple device are redundant (peer) controllers in an active-passive configuration.</span></span> <span data-ttu-id="70fcd-107">在指定的時間中，只能有一個控制器在主動模式，並處理所有磁碟和網路作業。</span><span class="sxs-lookup"><span data-stu-id="70fcd-107">At a given time, only one controller is active and is processing all the disk and network operations.</span></span> <span data-ttu-id="70fcd-108">另一個控制器處於被動模式。</span><span class="sxs-lookup"><span data-stu-id="70fcd-108">The other controller is in a passive mode.</span></span> <span data-ttu-id="70fcd-109">如果主動控制器故障，被動控制器會自動變成主動。</span><span class="sxs-lookup"><span data-stu-id="70fcd-109">If the active controller fails, the passive controller automatically becomes active.</span></span>

<span data-ttu-id="70fcd-110">本教學課程包含使用下列內容管理裝置控制器的逐步指示：</span><span class="sxs-lookup"><span data-stu-id="70fcd-110">This tutorial includes step-by-step instructions to manage the device controllers by using the:</span></span>

* <span data-ttu-id="70fcd-111">StorSimple 裝置管理員服務中，裝置的 [控制器] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="70fcd-111">**Controllers** blade for your device in the  StorSimple Device Manager service.</span></span>
* <span data-ttu-id="70fcd-112">Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="70fcd-112">Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="70fcd-113">我們建議您透過 StorSimple 裝置管理員服務管理裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-113">We recommend that you manage the device controllers via the  StorSimple Device Manager service.</span></span> <span data-ttu-id="70fcd-114">如果動作只能使用 Windows PowerShell for StorSimple 執行，本教學課程會記錄下來。</span><span class="sxs-lookup"><span data-stu-id="70fcd-114">If an action can only be performed by using Windows PowerShell for StorSimple, the tutorial makes a note of it.</span></span>

<span data-ttu-id="70fcd-115">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="70fcd-115">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="70fcd-116">重新啟動或關閉 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="70fcd-116">Restart or shut down a StorSimple device controller</span></span>
* <span data-ttu-id="70fcd-117">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="70fcd-117">Shut down a StorSimple device</span></span>
* <span data-ttu-id="70fcd-118">將 StorSimple 裝置重設為原廠預設值</span><span class="sxs-lookup"><span data-stu-id="70fcd-118">Reset your StorSimple device to factory defaults</span></span>

## <a name="restart-or-shut-down-a-single-controller"></a><span data-ttu-id="70fcd-119">重新啟動或關閉單一控制器</span><span class="sxs-lookup"><span data-stu-id="70fcd-119">Restart or shut down a single controller</span></span>
<span data-ttu-id="70fcd-120">一般系統作業並不需要重新啟動或關閉控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-120">A controller restart or shutdown is not required as a part of normal system operation.</span></span> <span data-ttu-id="70fcd-121">只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。</span><span class="sxs-lookup"><span data-stu-id="70fcd-121">Shutdown operations for a single device controller are common only in cases in which a failed device hardware component requires replacement.</span></span> <span data-ttu-id="70fcd-122">只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-122">A controller restart may also be required in a situation in which performance is affected by excessive memory usage or a malfunctioning controller.</span></span> <span data-ttu-id="70fcd-123">成功更換控制器之後，如果您想要啟用並測試更換的控制器，也可能需要重新啟動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-123">You may also need to restart a controller after a successful controller replacement, if you wish to enable and test the replaced controller.</span></span>

<span data-ttu-id="70fcd-124">假設被動控制器可用，重新啟動裝置並不會干擾連線的啟動器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-124">Restarting a device is not disruptive to connected initiators, assuming the passive controller is available.</span></span> <span data-ttu-id="70fcd-125">如果被動控制器不可用或已關閉，重新啟動主動控制器可能會導致服務中斷和停機。</span><span class="sxs-lookup"><span data-stu-id="70fcd-125">If a passive controller is not available or turned off, then restarting the active controller may result in the disruption of service and downtime.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="70fcd-126">**執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**</span><span class="sxs-lookup"><span data-stu-id="70fcd-126">**A running controller should never be physically removed as this would result in a loss of redundancy and an increased risk of downtime.**</span></span>
> * <span data-ttu-id="70fcd-127">下列程序只適用於 StorSimple 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-127">The following procedure applies only to the StorSimple physical device.</span></span> <span data-ttu-id="70fcd-128">如需有關如何啟動、停止和重新啟動 StorSimple 雲端設備的資訊，請參閱[使用雲端設備](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance)。</span><span class="sxs-lookup"><span data-stu-id="70fcd-128">For information about how to start, stop, and restart the StorSimple Cloud Appliance, see [Work with the cloud appliance](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).</span></span>

<span data-ttu-id="70fcd-129">您可以使用 StorSimple 裝置管理員服務或適用於 StorSimple 的 Windows PowerShell 的 Azure 入口網站重新啟動或關閉單一裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-129">You can restart or shut down a single device controller via the Azure portal of the  StorSimple Device Manager service or Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="70fcd-130">若要從 Azure 入口網站管理您的裝置控制器，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="70fcd-130">To manage your device controllers from the Azure portal, perform the following steps.</span></span>

#### <a name="to-restart-or-shut-down-a-controller-in-azure-portal"></a><span data-ttu-id="70fcd-131">若要在 Azure 入口網站中重新啟動或關閉控制器</span><span class="sxs-lookup"><span data-stu-id="70fcd-131">To restart or shut down a controller in Azure portal</span></span>
1. <span data-ttu-id="70fcd-132">請在 StorSimple 裝置管理員服務中，按一下 [裝置]。</span><span class="sxs-lookup"><span data-stu-id="70fcd-132">In your StorSimple Device Manager service, go to **Devices**.</span></span> <span data-ttu-id="70fcd-133">從裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-133">Select your device from the list of devices.</span></span> 

    ![選擇裝置](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. <span data-ttu-id="70fcd-135">移至 [設定] > [控制器]。</span><span class="sxs-lookup"><span data-stu-id="70fcd-135">Go to **Settings > Controllers**.</span></span>
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. <span data-ttu-id="70fcd-137">在 [控制器] 刀鋒視窗中，確認裝置上的兩個控制器狀態為 [狀況良好]。</span><span class="sxs-lookup"><span data-stu-id="70fcd-137">In the **Controllers** blade, verify that the status of both the controllers on your device is **Healthy**.</span></span> <span data-ttu-id="70fcd-138">選取控制器，以滑鼠右鍵按一下，然後選取 [重新啟動] 或 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="70fcd-138">Select a controller, right-click and then select **Restart** or **Shut down**.</span></span>

    ![選擇重新啟動或關閉 StorSimple 裝置控制器](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. <span data-ttu-id="70fcd-140">隨即會建立作業，以重新啟動或關閉控制器，若有適用的警告，也會於此顯示。</span><span class="sxs-lookup"><span data-stu-id="70fcd-140">A job is created to restart or shut down the controller and you are presented with applicable warnings, if any.</span></span> <span data-ttu-id="70fcd-141">若要監視重新啟動或關閉的情況，請移至 [服務] > [活動記錄]，然後根據服務專用的參數進行篩選。</span><span class="sxs-lookup"><span data-stu-id="70fcd-141">To monitor the restart or shutdown, go to **Service > Activity logs** and then filter by parameters specific to your service.</span></span> <span data-ttu-id="70fcd-142">如果控制器已關閉，您必須按下電源開關將控制器開啟。</span><span class="sxs-lookup"><span data-stu-id="70fcd-142">If a controller was shut down, then you will need to push the power button to turn on the controller to turn it on.</span></span>

#### <a name="to-restart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a><span data-ttu-id="70fcd-143">重新啟動或關閉 Windows PowerShell for StorSimple 中的控制器</span><span class="sxs-lookup"><span data-stu-id="70fcd-143">To restart or shut down a controller in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="70fcd-144">執行下列步驟，以從適用於 StorSimple 的 Windows PowerShell 關閉或重新啟動 StorSimple 裝置上的單一控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-144">Perform the following steps to shut down or restart a single controller on your StorSimple device from the Windows PowerShell for StorSimple.</span></span>

1. <span data-ttu-id="70fcd-145">透過序列主控台或 telnet 工作階段，從遠端電腦存取裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-145">Access the device via the serial console or a telnet session from a remote computer.</span></span> <span data-ttu-id="70fcd-146">遵循[使用 PuTTY 連接到裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)中的步驟，連接到控制器 0 或控制器 1。</span><span class="sxs-lookup"><span data-stu-id="70fcd-146">To connect to Controller 0 or Controller 1, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="70fcd-147">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="70fcd-147">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="70fcd-148">在橫幅訊息中，記下您已連接的控制器 (控制器 0 或控制器 1) 以及它是主動或被動 (待命) 控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-148">In the banner message, make a note of the controller you are connected to (Controller 0 or Controller 1) and whether it is the active or the passive (standby) controller.</span></span>
   
   * <span data-ttu-id="70fcd-149">若要關閉單一控制器，請在提示中輸入：</span><span class="sxs-lookup"><span data-stu-id="70fcd-149">To shut down a single controller, at the prompt, type:</span></span>
     
       `Stop-HcsController`
     
       <span data-ttu-id="70fcd-150">這會關閉您所連接的控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-150">This shuts down the controller that you are connected to.</span></span> <span data-ttu-id="70fcd-151">如果停止了主動控制器，則此裝置會容錯移轉至被動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-151">If you stop the active controller, then the device fails over to the passive controller.</span></span>

   * <span data-ttu-id="70fcd-152">若要重新啟動控制器，請在提示中輸入：</span><span class="sxs-lookup"><span data-stu-id="70fcd-152">To restart a controller, at the prompt, type:</span></span>
     
       `Restart-HcsController`
     
       <span data-ttu-id="70fcd-153">這會重新啟動您所連接的控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-153">This restarts the controller that you are connected to.</span></span> <span data-ttu-id="70fcd-154">如果您重新啟動主動控制器，它會在重新啟動之前容錯移轉到被動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-154">If you restart the active controller, it fails over to the passive controller before the restart.</span></span>

## <a name="shut-down-a-storsimple-device"></a><span data-ttu-id="70fcd-155">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="70fcd-155">Shut down a StorSimple device</span></span>

<span data-ttu-id="70fcd-156">本節說明如何從遠端電腦關閉執行中或失敗的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-156">This section explains how to shut down a running or a failed StorSimple device from a remote computer.</span></span> <span data-ttu-id="70fcd-157">裝置會在關閉兩個裝置控制器之後關閉。</span><span class="sxs-lookup"><span data-stu-id="70fcd-157">A device is turned off after both the device controllers are shut down.</span></span> <span data-ttu-id="70fcd-158">當裝置正在實際移動，或被帶離服務時，則已經完成裝置關閉。</span><span class="sxs-lookup"><span data-stu-id="70fcd-158">A device shutdown is done when the device is physically moved, or is taken out of service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70fcd-159">關閉裝置之前，請檢查裝置元件的健全狀態。</span><span class="sxs-lookup"><span data-stu-id="70fcd-159">Before you shut down the device, check the health of the device components.</span></span> <span data-ttu-id="70fcd-160">瀏覽至您的裝置，然後按一下 [設定] > [硬體健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="70fcd-160">Navigate to your device and then click **Settings > Hardware health**.</span></span> <span data-ttu-id="70fcd-161">在 [狀態與硬體健康狀態] 刀鋒視窗中，確認所有元件的 LED 狀態皆為綠色。</span><span class="sxs-lookup"><span data-stu-id="70fcd-161">In the **Status and hardware health** blade, verify that the LED status of all the components is green.</span></span> <span data-ttu-id="70fcd-162">只有狀況良好的裝置才會有綠色的狀態。</span><span class="sxs-lookup"><span data-stu-id="70fcd-162">Only a healthy device has a green status.</span></span> <span data-ttu-id="70fcd-163">如果您的裝置正在關閉以更換故障的元件，您會看到個別元件的失敗 (紅色) 或降級 (黃色) 狀態。</span><span class="sxs-lookup"><span data-stu-id="70fcd-163">If your device is being shut down to replace a malfunctioning component, you will see a failed (red) or a degraded (yellow) status for the respective component(s).</span></span>


#### <a name="to-shut-down-a-storsimple-device"></a><span data-ttu-id="70fcd-164">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="70fcd-164">To shut down a StorSimple device</span></span>

1. <span data-ttu-id="70fcd-165">透過 [重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller) 程序，識別和關閉裝置上的被動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-165">Use the [restart or shut down a controller](#restart-or-shut-down-a-single-controller) procedure to identify and shut down the passive controller on your device.</span></span> <span data-ttu-id="70fcd-166">您可以在 Azure 入口網站或適用於 StorSimple 的 Windows PowerShell 中執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="70fcd-166">You can perform this operation in the Azure portal or in Windows PowerShell for StorSimple.</span></span>
2. <span data-ttu-id="70fcd-167">重複上述步驟來關閉主動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-167">Repeat the above step to shut down the active controller.</span></span>
3. <span data-ttu-id="70fcd-168">您現在必須查看裝置的背板。</span><span class="sxs-lookup"><span data-stu-id="70fcd-168">You must now look at the back plane of the device.</span></span> <span data-ttu-id="70fcd-169">完全關閉兩個控制器之後，兩個控制器上的狀態 Led 應該為閃爍的紅色。</span><span class="sxs-lookup"><span data-stu-id="70fcd-169">After the two controllers are completely shut down, the status LEDs on both the controllers should be blinking red.</span></span> <span data-ttu-id="70fcd-170">如果您需要在此時將裝置完全關閉，請將電源和冷卻模組 (PCM) 上的電源開關切換為 OFF 的位置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-170">If you need to turn off the device completely at this time, flip the power switches on both Power and Cooling Modules (PCMs) to the OFF position.</span></span> <span data-ttu-id="70fcd-171">這樣可以關閉裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-171">This should turn off the device.</span></span>

## <a name="reset-the-device-to-factory-default-settings"></a><span data-ttu-id="70fcd-172">將裝置重設為出廠預設設定。</span><span class="sxs-lookup"><span data-stu-id="70fcd-172">Reset the device to factory default settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70fcd-173">如果您需要將裝置重設為原廠預設設定，請聯絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="70fcd-173">If you need to reset your device to factory default settings, contact Microsoft Support.</span></span> <span data-ttu-id="70fcd-174">以下所述的程序，應只用於搭配 Microsoft 支援服務時使用。</span><span class="sxs-lookup"><span data-stu-id="70fcd-174">The procedure described below should be used only in conjunction with Microsoft Support.</span></span>

<span data-ttu-id="70fcd-175">此程序描述如何將 Microsoft Azure StorSimple 裝置重設為使用 Windows PowerShell for StorSimple 的出廠預設設定。</span><span class="sxs-lookup"><span data-stu-id="70fcd-175">This procedure describes how to reset your Microsoft Azure StorSimple device to factory default settings using Windows PowerShell for StorSimple.</span></span>
<span data-ttu-id="70fcd-176">根據預設，重設裝置會從整個叢集移除所有資料和設定。</span><span class="sxs-lookup"><span data-stu-id="70fcd-176">Resetting a device removes all data and settings from the entire cluster by default.</span></span>

<span data-ttu-id="70fcd-177">執行下列步驟來將 Microsoft Azure StorSimple 裝置重設為出廠預設設定：</span><span class="sxs-lookup"><span data-stu-id="70fcd-177">Perform the following steps to reset your Microsoft Azure StorSimple device to factory default settings:</span></span>

### <a name="to-reset-the-device-to-default-settings-in-windows-powershell-for-storsimple"></a><span data-ttu-id="70fcd-178">將裝置重設為 Windows PowerShell for StorSimple 中的預設設定</span><span class="sxs-lookup"><span data-stu-id="70fcd-178">To reset the device to default settings in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="70fcd-179">透過裝置的序列主控台存取裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-179">Access the device through its serial console.</span></span> <span data-ttu-id="70fcd-180">檢查橫幅訊息以確保您已連接到**主動**控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-180">Check the banner message to ensure that you are connected to the **Active** controller.</span></span>
2. <span data-ttu-id="70fcd-181">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="70fcd-181">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="70fcd-182">在提示中，輸入下列命令來重設整個叢集，移除所有資料、中繼資料和控制器設定︰</span><span class="sxs-lookup"><span data-stu-id="70fcd-182">At the prompt, type the following command to reset the entire cluster, removing all data, metadata, and controller settings:</span></span>
   
    `Reset-HcsFactoryDefault`
   
    <span data-ttu-id="70fcd-183">若要改為重設單一控制站，請使用 [Reset-HcsFactoryDefault`-scope` Cmdlet 搭配 ](http://technet.microsoft.com/library/dn688132.aspx) 參數。)</span><span class="sxs-lookup"><span data-stu-id="70fcd-183">To instead reset a single controller, use the  [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet with the `-scope` parameter.)</span></span>
   
    <span data-ttu-id="70fcd-184">系統會重新啟動多次。</span><span class="sxs-lookup"><span data-stu-id="70fcd-184">The system will reboot multiple times.</span></span> <span data-ttu-id="70fcd-185">重設成功完成時，系統將會通知您。</span><span class="sxs-lookup"><span data-stu-id="70fcd-185">You will be notified when the reset has successfully completed.</span></span> <span data-ttu-id="70fcd-186">根據系統模型，8100 裝置可能需要 45-60 分鐘來完成此程序，而 8600 需要 60-90 分鐘。</span><span class="sxs-lookup"><span data-stu-id="70fcd-186">Depending on the system model, it can take 45-60 minutes for an 8100 device and 60-90 minutes for an 8600 to finish this process.</span></span>
   
## <a name="questions-and-answers-about-managing-device-controllers"></a><span data-ttu-id="70fcd-187">有關管理裝置控制器的問題與解答</span><span class="sxs-lookup"><span data-stu-id="70fcd-187">Questions and answers about managing device controllers</span></span>
<span data-ttu-id="70fcd-188">在本節中，我們摘要說明一些有關管理 StorSimple 裝置控制器的常見問題。</span><span class="sxs-lookup"><span data-stu-id="70fcd-188">In this section, we have summarized some of the frequently asked questions regarding managing StorSimple device controllers.</span></span>

<span data-ttu-id="70fcd-189">**問：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-189">**Q.**</span></span> <span data-ttu-id="70fcd-190">如果裝置上的兩個控制器都狀況良好且已開啟，而我重新啟動或關閉主動控制器，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="70fcd-190">What happens if both the controllers on my device are healthy and turned on and I restart or shut down the active controller?</span></span>

<span data-ttu-id="70fcd-191">**答：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-191">**A.**</span></span> <span data-ttu-id="70fcd-192">如果裝置上的兩個控制器皆狀況良好且已開啟，您會收到確認提示。</span><span class="sxs-lookup"><span data-stu-id="70fcd-192">If both the controllers on your device are healthy and turned on, you are prompted for confirmation.</span></span> <span data-ttu-id="70fcd-193">您可以選擇：</span><span class="sxs-lookup"><span data-stu-id="70fcd-193">You may choose to:</span></span>

* <span data-ttu-id="70fcd-194">**重新啟動主動控制器** – 您會收到通知，告知您重新啟動主動控制器將使裝置容錯移轉到被動控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-194">**Restart the active controller** – You are notified that restarting an active controller caused the device to fail over to the passive controller.</span></span> <span data-ttu-id="70fcd-195">控制器會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="70fcd-195">The controller restarts.</span></span>
* <span data-ttu-id="70fcd-196">**關閉主動控制器** – 您會收到通知，告知您關閉主動控制器將導致停機。</span><span class="sxs-lookup"><span data-stu-id="70fcd-196">**Shut down an active controller** – You are notified that shutting down an active controller results in downtime.</span></span> <span data-ttu-id="70fcd-197">您也必須按下裝置上的電源開關，以開啟控制器。</span><span class="sxs-lookup"><span data-stu-id="70fcd-197">You also need to push the power button on the device to turn on the controller.</span></span>

<span data-ttu-id="70fcd-198">**問：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-198">**Q.**</span></span> <span data-ttu-id="70fcd-199">如果裝置上的被動控制器無法使用或已關閉，而我重新啟動或關閉主動控制器，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="70fcd-199">What happens if the passive controller on my device is unavailable or turned off and I restart or shut down the active controller?</span></span>

<span data-ttu-id="70fcd-200">**答：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-200">**A.**</span></span> <span data-ttu-id="70fcd-201">如果裝置上的被動控制器無法使用或已關閉，而您選擇：</span><span class="sxs-lookup"><span data-stu-id="70fcd-201">If the passive controller on your device is unavailable or turned off, and you choose to:</span></span>

* <span data-ttu-id="70fcd-202">**重新啟動主動控制器** – 您會收到通知，告知您繼續執行作業會導致服務暫時中斷，而且您會收到確認提示。</span><span class="sxs-lookup"><span data-stu-id="70fcd-202">**Restart the active controller** – You are notified that continuing the operation will result in a temporary disruption of the service, and you are prompted for confirmation.</span></span>
* <span data-ttu-id="70fcd-203">**關閉主動控制器** – 您會收到通知，告知您繼續作業將導致停機。</span><span class="sxs-lookup"><span data-stu-id="70fcd-203">**Shut down an active controller** – You are notified that continuing the operation results in downtime.</span></span> <span data-ttu-id="70fcd-204">您也必須按下一個或兩個控制器的電源開關，以開啟裝置。</span><span class="sxs-lookup"><span data-stu-id="70fcd-204">You also need to push the power button on one or both controllers to turn on the device.</span></span> <span data-ttu-id="70fcd-205">系統會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="70fcd-205">You are prompted for confirmation.</span></span>

<span data-ttu-id="70fcd-206">**問：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-206">**Q.**</span></span> <span data-ttu-id="70fcd-207">何時控制器重新啟動或關機會無法進行？</span><span class="sxs-lookup"><span data-stu-id="70fcd-207">When does the controller restart or shutdown fails to progress?</span></span>

<span data-ttu-id="70fcd-208">**答：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-208">**A.**</span></span> <span data-ttu-id="70fcd-209">重新啟動或關閉控制器可能會在下列情況下失敗：</span><span class="sxs-lookup"><span data-stu-id="70fcd-209">Restarting or shutting down a controller may fail if:</span></span>

* <span data-ttu-id="70fcd-210">裝置更新進行中。</span><span class="sxs-lookup"><span data-stu-id="70fcd-210">A device update is in progress.</span></span>
* <span data-ttu-id="70fcd-211">控制器重新啟動已在進行中。</span><span class="sxs-lookup"><span data-stu-id="70fcd-211">A controller restart is already in progress.</span></span>
* <span data-ttu-id="70fcd-212">控制器關閉已在進行中。</span><span class="sxs-lookup"><span data-stu-id="70fcd-212">A controller shutdown is already in progress.</span></span>

<span data-ttu-id="70fcd-213">**問：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-213">**Q.**</span></span> <span data-ttu-id="70fcd-214">您如何判斷控制器已重新啟動或關閉？</span><span class="sxs-lookup"><span data-stu-id="70fcd-214">How can you figure out if a controller was restarted or shut down?</span></span>

<span data-ttu-id="70fcd-215">**答：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-215">**A.**</span></span> <span data-ttu-id="70fcd-216">您可以在 [控制器] 刀鋒視窗上檢查控制器狀態。</span><span class="sxs-lookup"><span data-stu-id="70fcd-216">You can check the controller status on Controller blade.</span></span> <span data-ttu-id="70fcd-217">控制器狀態會指出控制器是否正在重新啟動或關閉。</span><span class="sxs-lookup"><span data-stu-id="70fcd-217">The controller status will indicate whether a controller is in the process of restarting or shutting down.</span></span> <span data-ttu-id="70fcd-218">此外，如果控制器已重新啟動或關閉，[警示] 刀鋒視窗會包含資訊警示。</span><span class="sxs-lookup"><span data-stu-id="70fcd-218">Additionally, the **Alerts** blade contain an informational alert if the controller is restarted or shut down.</span></span> <span data-ttu-id="70fcd-219">控制器重新啟動和關閉作業也會記錄在活動記錄中。</span><span class="sxs-lookup"><span data-stu-id="70fcd-219">The controller restart and shutdown operations are also recorded in the acitivity logs.</span></span> <span data-ttu-id="70fcd-220">如需有關活動記錄的詳細資訊，請移至[檢視活動記錄](storsimple-8000-service-dashboard.md#view-the-activity-logs)。</span><span class="sxs-lookup"><span data-stu-id="70fcd-220">For more information about acitivity logs, go to [View the activity logs](storsimple-8000-service-dashboard.md#view-the-activity-logs).</span></span>

<span data-ttu-id="70fcd-221">**問：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-221">**Q.**</span></span> <span data-ttu-id="70fcd-222">控制器容錯移轉會不會對 I/O 造成任何影響？</span><span class="sxs-lookup"><span data-stu-id="70fcd-222">Is there any impact to the I/O as a result of controller failover?</span></span>

<span data-ttu-id="70fcd-223">**答：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-223">**A.**</span></span> <span data-ttu-id="70fcd-224">啟動器和主動控制器之間的 TCP 連接將會因為控制器容錯移轉而重設，但會在被動控制器繼續作業時重新建立。</span><span class="sxs-lookup"><span data-stu-id="70fcd-224">The TCP connections between initiators and active controller will be reset as a result of controller failover, but will be reestablished when the passive controller assumes operation.</span></span> <span data-ttu-id="70fcd-225">在這項作業的過程中，啟動器與裝置之間的 I/O 活動中可能會有暫時的 (少於 30 秒) 暫停。</span><span class="sxs-lookup"><span data-stu-id="70fcd-225">There may be a temporary (less than 30 seconds) pause in I/O activity between initiators and the device during the course of this operation.</span></span>

<span data-ttu-id="70fcd-226">**問：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-226">**Q.**</span></span> <span data-ttu-id="70fcd-227">如何在控制器關閉並遭移除後，將控制器傳回給服務？</span><span class="sxs-lookup"><span data-stu-id="70fcd-227">How do I return my controller to service after it has been shut down and removed?</span></span>

<span data-ttu-id="70fcd-228">**答：**</span><span class="sxs-lookup"><span data-stu-id="70fcd-228">**A.**</span></span> <span data-ttu-id="70fcd-229">若要將控制器傳回給服務，您必須依照 [更換 StorSimple 裝置上的控制器模組](storsimple-8000-controller-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="70fcd-229">To return a controller to service, you must insert it into the chassis as described in [Replace a controller module on your StorSimple device](storsimple-8000-controller-replacement.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70fcd-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70fcd-230">Next steps</span></span>
* <span data-ttu-id="70fcd-231">如果發生任何無法使用本教學課程中所列之程序解決的 StorSimple 裝置控制器相關問題，請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="70fcd-231">If you encounter any issues with your StorSimple device controllers that you cannot resolve by using the procedures listed in this tutorial, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="70fcd-232">若要深入了解使用 StorSimple 裝置管理員服務的方式，請移至[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="70fcd-232">To learn more about using the  StorSimple Device Manager service, go to [Use the  StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

