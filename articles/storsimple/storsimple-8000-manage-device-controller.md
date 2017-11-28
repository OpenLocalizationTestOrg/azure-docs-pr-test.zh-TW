---
title: "aaaManage StorSimple 8000 系列裝置控制器 |Microsoft 文件"
description: "了解 toostop，重新啟動、 關機或重設您的 StorSimple 裝置控制站的方式。"
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
ms.openlocfilehash: 5c59582b7ccf7cfeae9e7efbd0e4df9dc1d3871c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a><span data-ttu-id="7a93c-103">管理 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="7a93c-103">Manage your StorSimple device controllers</span></span>

## <a name="overview"></a><span data-ttu-id="7a93c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7a93c-104">Overview</span></span>

<span data-ttu-id="7a93c-105">本教學課程描述 hello 可在您的 StorSimple 裝置控制站執行的不同作業。</span><span class="sxs-lookup"><span data-stu-id="7a93c-105">This tutorial describes hello different operations that can be performed on your StorSimple device controllers.</span></span> <span data-ttu-id="7a93c-106">您的 StorSimple 裝置中的 hello 控制站會在主動-被動組態的備援 （對等） 控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-106">hello controllers in your StorSimple device are redundant (peer) controllers in an active-passive configuration.</span></span> <span data-ttu-id="7a93c-107">在指定的時間，只能有一個控制器為作用中，並處理所有的 hello 磁碟和網路作業。</span><span class="sxs-lookup"><span data-stu-id="7a93c-107">At a given time, only one controller is active and is processing all hello disk and network operations.</span></span> <span data-ttu-id="7a93c-108">hello 另一個控制器處於被動模式。</span><span class="sxs-lookup"><span data-stu-id="7a93c-108">hello other controller is in a passive mode.</span></span> <span data-ttu-id="7a93c-109">Hello 主動控制器失效，如果 hello 被動控制器會自動變成使用中。</span><span class="sxs-lookup"><span data-stu-id="7a93c-109">If hello active controller fails, hello passive controller automatically becomes active.</span></span>

<span data-ttu-id="7a93c-110">本教學課程使用包含 toomanage hello 裝置控制站的逐步指示:</span><span class="sxs-lookup"><span data-stu-id="7a93c-110">This tutorial includes step-by-step instructions toomanage hello device controllers by using the:</span></span>

* <span data-ttu-id="7a93c-111">**控制站**hello StorSimple 裝置管理員服務在裝置的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7a93c-111">**Controllers** blade for your device in hello  StorSimple Device Manager service.</span></span>
* <span data-ttu-id="7a93c-112">Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="7a93c-112">Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="7a93c-113">我們建議您管理透過 hello StorSimple 裝置管理員服務的 hello 裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-113">We recommend that you manage hello device controllers via hello  StorSimple Device Manager service.</span></span> <span data-ttu-id="7a93c-114">如果只可以使用 Windows PowerShell for StorSimple 執行某個動作，hello 教學課程還會記錄下來。</span><span class="sxs-lookup"><span data-stu-id="7a93c-114">If an action can only be performed by using Windows PowerShell for StorSimple, hello tutorial makes a note of it.</span></span>

<span data-ttu-id="7a93c-115">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="7a93c-115">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="7a93c-116">重新啟動或關閉 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="7a93c-116">Restart or shut down a StorSimple device controller</span></span>
* <span data-ttu-id="7a93c-117">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="7a93c-117">Shut down a StorSimple device</span></span>
* <span data-ttu-id="7a93c-118">重設您的 StorSimple 裝置 toofactory 預設值</span><span class="sxs-lookup"><span data-stu-id="7a93c-118">Reset your StorSimple device toofactory defaults</span></span>

## <a name="restart-or-shut-down-a-single-controller"></a><span data-ttu-id="7a93c-119">重新啟動或關閉單一控制器</span><span class="sxs-lookup"><span data-stu-id="7a93c-119">Restart or shut down a single controller</span></span>
<span data-ttu-id="7a93c-120">一般系統作業並不需要重新啟動或關閉控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-120">A controller restart or shutdown is not required as a part of normal system operation.</span></span> <span data-ttu-id="7a93c-121">只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。</span><span class="sxs-lookup"><span data-stu-id="7a93c-121">Shutdown operations for a single device controller are common only in cases in which a failed device hardware component requires replacement.</span></span> <span data-ttu-id="7a93c-122">只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-122">A controller restart may also be required in a situation in which performance is affected by excessive memory usage or a malfunctioning controller.</span></span> <span data-ttu-id="7a93c-123">您也可能需要 toorestart 控制站之後在成功更換控制器，如果您希望 tooenable 測試 hello 取代控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-123">You may also need toorestart a controller after a successful controller replacement, if you wish tooenable and test hello replaced controller.</span></span>

<span data-ttu-id="7a93c-124">重新啟動的裝置不干擾 tooconnected 啟動器，假設 hello 被動控制站可用。</span><span class="sxs-lookup"><span data-stu-id="7a93c-124">Restarting a device is not disruptive tooconnected initiators, assuming hello passive controller is available.</span></span> <span data-ttu-id="7a93c-125">如果是被動控制器無法使用或已關閉，然後重新啟動 hello active 控制器可能會導致 hello 服務中斷和停機時間。</span><span class="sxs-lookup"><span data-stu-id="7a93c-125">If a passive controller is not available or turned off, then restarting hello active controller may result in hello disruption of service and downtime.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="7a93c-126">**執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**</span><span class="sxs-lookup"><span data-stu-id="7a93c-126">**A running controller should never be physically removed as this would result in a loss of redundancy and an increased risk of downtime.**</span></span>
> * <span data-ttu-id="7a93c-127">hello 下列程序適用於僅 toohello StorSimple 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="7a93c-127">hello following procedure applies only toohello StorSimple physical device.</span></span> <span data-ttu-id="7a93c-128">如需有關如何 toostart、 停止及重新啟動 hello StorSimple 雲端應用裝置，請參閱資訊[搭配 hello 雲端應用裝置](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance)。</span><span class="sxs-lookup"><span data-stu-id="7a93c-128">For information about how toostart, stop, and restart hello StorSimple Cloud Appliance, see [Work with hello cloud appliance](storsimple-8000-cloud-appliance-u2.md##work-with-the-storsimple-cloud-appliance).</span></span>

<span data-ttu-id="7a93c-129">您可以重新啟動或關閉透過 hello hello StorSimple 裝置管理員服務或 Windows PowerShell 的 Azure 入口網站的單一裝置控制站 for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="7a93c-129">You can restart or shut down a single device controller via hello Azure portal of hello  StorSimple Device Manager service or Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="7a93c-130">toomanage hello Azure 入口網站，從您的裝置控制站執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="7a93c-130">toomanage your device controllers from hello Azure portal, perform hello following steps.</span></span>

#### <a name="toorestart-or-shut-down-a-controller-in-azure-portal"></a><span data-ttu-id="7a93c-131">toorestart 或 Azure 入口網站中的控制站關機</span><span class="sxs-lookup"><span data-stu-id="7a93c-131">toorestart or shut down a controller in Azure portal</span></span>
1. <span data-ttu-id="7a93c-132">在您的 StorSimple 裝置管理員服務移過**裝置**。</span><span class="sxs-lookup"><span data-stu-id="7a93c-132">In your StorSimple Device Manager service, go too**Devices**.</span></span> <span data-ttu-id="7a93c-133">從裝置 hello 清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7a93c-133">Select your device from hello list of devices.</span></span> 

    ![選擇裝置](./media/storsimple-8000-manage-device-controller/manage-controller1.png)

2. <span data-ttu-id="7a93c-135">跳過**設定 > 控制站**。</span><span class="sxs-lookup"><span data-stu-id="7a93c-135">Go too**Settings > Controllers**.</span></span>
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-8000-manage-device-controller/manage-controller2.png)
3. <span data-ttu-id="7a93c-137">在 hello**控制器**刀鋒視窗中，確認您的裝置上的兩個 hello 控制器的 hello 狀態為**狀況良好**。</span><span class="sxs-lookup"><span data-stu-id="7a93c-137">In hello **Controllers** blade, verify that hello status of both hello controllers on your device is **Healthy**.</span></span> <span data-ttu-id="7a93c-138">選取控制器，以滑鼠右鍵按一下，然後選取 [重新啟動] 或 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="7a93c-138">Select a controller, right-click and then select **Restart** or **Shut down**.</span></span>

    ![選擇重新啟動或關閉 StorSimple 裝置控制器](./media/storsimple-8000-manage-device-controller/manage-controller3.png)

4. <span data-ttu-id="7a93c-140">工作建立 toorestart 或關閉 hello 控制器，您會有適用於警告，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="7a93c-140">A job is created toorestart or shut down hello controller and you are presented with applicable warnings, if any.</span></span> <span data-ttu-id="7a93c-141">toomonitor hello 重新啟動或關機，跳過**服務 > 活動記錄**然後篩選參數特定 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="7a93c-141">toomonitor hello restart or shutdown, go too**Service > Activity logs** and then filter by parameters specific tooyour service.</span></span> <span data-ttu-id="7a93c-142">如果控制器已關閉，則您必須在 hello 控制器 tooturn toopush hello 電源按鈕 tooturn 其上。</span><span class="sxs-lookup"><span data-stu-id="7a93c-142">If a controller was shut down, then you will need toopush hello power button tooturn on hello controller tooturn it on.</span></span>

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7a93c-143">toorestart 或關機的控制站，在 Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="7a93c-143">toorestart or shut down a controller in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="7a93c-144">StorSimple 的重新啟動 StorSimple 裝置 hello Windows PowerShell 從單一控制器或執行向下遵循步驟 tooshut hello。</span><span class="sxs-lookup"><span data-stu-id="7a93c-144">Perform hello following steps tooshut down or restart a single controller on your StorSimple device from hello Windows PowerShell for StorSimple.</span></span>

1. <span data-ttu-id="7a93c-145">存取 hello hello 序列主控台或 telnet 工作階段從遠端電腦的裝置。</span><span class="sxs-lookup"><span data-stu-id="7a93c-145">Access hello device via hello serial console or a telnet session from a remote computer.</span></span> <span data-ttu-id="7a93c-146">tooconnect tooController 0 或控制器 1，請依照下列中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="7a93c-146">tooconnect tooController 0 or Controller 1, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="7a93c-147">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="7a93c-147">In hello serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="7a93c-148">在 hello 橫幅訊息中，記下過，您所連接的 hello 控制器 （控制器 0 或控制器 1），以及是否使用中的 hello 被動 （待命） 控制站。</span><span class="sxs-lookup"><span data-stu-id="7a93c-148">In hello banner message, make a note of hello controller you are connected too(Controller 0 or Controller 1) and whether it is hello active or hello passive (standby) controller.</span></span>
   
   * <span data-ttu-id="7a93c-149">tooshut 關閉單一控制器，在 hello 提示字元，輸入：</span><span class="sxs-lookup"><span data-stu-id="7a93c-149">tooshut down a single controller, at hello prompt, type:</span></span>
     
       `Stop-HcsController`
     
       <span data-ttu-id="7a93c-150">這會關閉您所連接的 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="7a93c-150">This shuts down hello controller that you are connected to.</span></span> <span data-ttu-id="7a93c-151">如果您停止 hello 作用中控制器，hello 裝置容錯移轉 toohello 被動控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-151">If you stop hello active controller, then hello device fails over toohello passive controller.</span></span>

   * <span data-ttu-id="7a93c-152">toorestart 控制站，在 hello 提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="7a93c-152">toorestart a controller, at hello prompt, type:</span></span>
     
       `Restart-HcsController`
     
       <span data-ttu-id="7a93c-153">這會重新啟動您所連接的 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="7a93c-153">This restarts hello controller that you are connected to.</span></span> <span data-ttu-id="7a93c-154">如果您重新啟動 hello 作用中控制器，它會容錯移轉 toohello 被動控制站之前 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="7a93c-154">If you restart hello active controller, it fails over toohello passive controller before hello restart.</span></span>

## <a name="shut-down-a-storsimple-device"></a><span data-ttu-id="7a93c-155">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="7a93c-155">Shut down a StorSimple device</span></span>

<span data-ttu-id="7a93c-156">本章節將說明如何 tooshut 關閉執行中或失敗的 StorSimple 裝置，從遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="7a93c-156">This section explains how tooshut down a running or a failed StorSimple device from a remote computer.</span></span> <span data-ttu-id="7a93c-157">兩個 hello 裝置控制器都關閉之後，裝置已關閉。</span><span class="sxs-lookup"><span data-stu-id="7a93c-157">A device is turned off after both hello device controllers are shut down.</span></span> <span data-ttu-id="7a93c-158">Hello 裝置實際移動，或帶離服務時，是完成裝置關機。</span><span class="sxs-lookup"><span data-stu-id="7a93c-158">A device shutdown is done when hello device is physically moved, or is taken out of service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a93c-159">您關閉 hello 裝置之前，請檢查 hello hello 裝置元件健全狀況。</span><span class="sxs-lookup"><span data-stu-id="7a93c-159">Before you shut down hello device, check hello health of hello device components.</span></span> <span data-ttu-id="7a93c-160">導覽 tooyour 裝置，然後按一下**設定 > 硬體健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="7a93c-160">Navigate tooyour device and then click **Settings > Hardware health**.</span></span> <span data-ttu-id="7a93c-161">在 hello**狀態和硬體的健全狀況**刀鋒視窗中，確認所有 hello 元件 hello LED 狀態為綠色。</span><span class="sxs-lookup"><span data-stu-id="7a93c-161">In hello **Status and hardware health** blade, verify that hello LED status of all hello components is green.</span></span> <span data-ttu-id="7a93c-162">只有狀況良好的裝置才會有綠色的狀態。</span><span class="sxs-lookup"><span data-stu-id="7a93c-162">Only a healthy device has a green status.</span></span> <span data-ttu-id="7a93c-163">如果您的裝置關機 tooreplace 的故障元件時，您會看到故障 （紅色） 或降級 （黃色） 狀態 hello 個別元件。</span><span class="sxs-lookup"><span data-stu-id="7a93c-163">If your device is being shut down tooreplace a malfunctioning component, you will see a failed (red) or a degraded (yellow) status for hello respective component(s).</span></span>


#### <a name="tooshut-down-a-storsimple-device"></a><span data-ttu-id="7a93c-164">tooshut StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="7a93c-164">tooshut down a StorSimple device</span></span>

1. <span data-ttu-id="7a93c-165">使用 hello[重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller)程序 tooidentify 並關機 hello 裝置上的被動控制器。</span><span class="sxs-lookup"><span data-stu-id="7a93c-165">Use hello [restart or shut down a controller](#restart-or-shut-down-a-single-controller) procedure tooidentify and shut down hello passive controller on your device.</span></span> <span data-ttu-id="7a93c-166">您可以針對 StorSimple hello Azure 入口網站或 Windows PowerShell 中執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="7a93c-166">You can perform this operation in hello Azure portal or in Windows PowerShell for StorSimple.</span></span>
2. <span data-ttu-id="7a93c-167">重複上述步驟 tooshut 向 hello 作用中控制器的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a93c-167">Repeat hello above step tooshut down hello active controller.</span></span>
3. <span data-ttu-id="7a93c-168">您必須立即查看 hello 回 hello 裝置面板。</span><span class="sxs-lookup"><span data-stu-id="7a93c-168">You must now look at hello back plane of hello device.</span></span> <span data-ttu-id="7a93c-169">Hello 兩個控制器都關閉之後，hello 兩個 hello 控制器狀態 Led 應閃爍紅燈。</span><span class="sxs-lookup"><span data-stu-id="7a93c-169">After hello two controllers are completely shut down, hello status LEDs on both hello controllers should be blinking red.</span></span> <span data-ttu-id="7a93c-170">如果您完全在這個階段需要關閉裝置 hello tooturn 上電源和冷卻模組 (Pcm), 翻轉 hello 電源開關 toohello OFF 位置。</span><span class="sxs-lookup"><span data-stu-id="7a93c-170">If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.</span></span> <span data-ttu-id="7a93c-171">這應該關閉 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7a93c-171">This should turn off hello device.</span></span>

## <a name="reset-hello-device-toofactory-default-settings"></a><span data-ttu-id="7a93c-172">重設 hello 裝置 toofactory 預設值</span><span class="sxs-lookup"><span data-stu-id="7a93c-172">Reset hello device toofactory default settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a93c-173">如果您需要 tooreset 裝置 toofactory 預設設定，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="7a93c-173">If you need tooreset your device toofactory default settings, contact Microsoft Support.</span></span> <span data-ttu-id="7a93c-174">hello 如下所述的程序只應該用於搭配 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="7a93c-174">hello procedure described below should be used only in conjunction with Microsoft Support.</span></span>

<span data-ttu-id="7a93c-175">此程序描述如何 tooreset 您 Microsoft Azure StorSimple 裝置 toofactory 的預設設定使用 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="7a93c-175">This procedure describes how tooreset your Microsoft Azure StorSimple device toofactory default settings using Windows PowerShell for StorSimple.</span></span>
<span data-ttu-id="7a93c-176">重設裝置移除所有資料和設定預設的 hello 整個叢集。</span><span class="sxs-lookup"><span data-stu-id="7a93c-176">Resetting a device removes all data and settings from hello entire cluster by default.</span></span>

<span data-ttu-id="7a93c-177">您的 Microsoft Azure StorSimple 裝置 toofactory 預設設定執行下列步驟 tooreset hello:</span><span class="sxs-lookup"><span data-stu-id="7a93c-177">Perform hello following steps tooreset your Microsoft Azure StorSimple device toofactory default settings:</span></span>

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a><span data-ttu-id="7a93c-178">tooreset hello toodefault 的裝置設定 Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="7a93c-178">tooreset hello device toodefault settings in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="7a93c-179">透過序列主控台存取 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7a93c-179">Access hello device through its serial console.</span></span> <span data-ttu-id="7a93c-180">請檢查您所連接的 toohello hello 橫幅訊息 tooensure **Active**控制站。</span><span class="sxs-lookup"><span data-stu-id="7a93c-180">Check hello banner message tooensure that you are connected toohello **Active** controller.</span></span>
2. <span data-ttu-id="7a93c-181">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="7a93c-181">In hello serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="7a93c-182">在 hello 提示中輸入下列命令 tooreset hello 整個叢集，移除所有的資料、 中繼資料及控制器設定 hello:</span><span class="sxs-lookup"><span data-stu-id="7a93c-182">At hello prompt, type hello following command tooreset hello entire cluster, removing all data, metadata, and controller settings:</span></span>
   
    `Reset-HcsFactoryDefault`
   
    <span data-ttu-id="7a93c-183">tooinstead 重設一個控制器，請使用 hello [Reset-hcsfactorydefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet 搭配 hello`-scope`參數。)</span><span class="sxs-lookup"><span data-stu-id="7a93c-183">tooinstead reset a single controller, use hello  [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet with hello `-scope` parameter.)</span></span>
   
    <span data-ttu-id="7a93c-184">hello 系統將會重新啟動多次。</span><span class="sxs-lookup"><span data-stu-id="7a93c-184">hello system will reboot multiple times.</span></span> <span data-ttu-id="7a93c-185">Hello 重設已順利完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="7a93c-185">You will be notified when hello reset has successfully completed.</span></span> <span data-ttu-id="7a93c-186">根據 hello 系統模型，它可能需要 45-60 分鐘 8100 裝置和 60-90 分鐘的 8600 toofinish 此程序。</span><span class="sxs-lookup"><span data-stu-id="7a93c-186">Depending on hello system model, it can take 45-60 minutes for an 8100 device and 60-90 minutes for an 8600 toofinish this process.</span></span>
   
## <a name="questions-and-answers-about-managing-device-controllers"></a><span data-ttu-id="7a93c-187">有關管理裝置控制器的問題與解答</span><span class="sxs-lookup"><span data-stu-id="7a93c-187">Questions and answers about managing device controllers</span></span>
<span data-ttu-id="7a93c-188">在本節中，我們有摘要一些 hello 常見問題集有關管理 StorSimple 裝置控制站。</span><span class="sxs-lookup"><span data-stu-id="7a93c-188">In this section, we have summarized some of hello frequently asked questions regarding managing StorSimple device controllers.</span></span>

<span data-ttu-id="7a93c-189">**問：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-189">**Q.**</span></span> <span data-ttu-id="7a93c-190">如果兩者 hello 我的裝置上控制站，會發生什麼情況都是狀況良好並已在與我重新啟動或關閉 hello 主動控制器？</span><span class="sxs-lookup"><span data-stu-id="7a93c-190">What happens if both hello controllers on my device are healthy and turned on and I restart or shut down hello active controller?</span></span>

<span data-ttu-id="7a93c-191">**答：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-191">**A.**</span></span> <span data-ttu-id="7a93c-192">如果您的裝置上的兩個 hello 控制器皆狀況良好並已 on 時，系統會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="7a93c-192">If both hello controllers on your device are healthy and turned on, you are prompted for confirmation.</span></span> <span data-ttu-id="7a93c-193">您可以選擇：</span><span class="sxs-lookup"><span data-stu-id="7a93c-193">You may choose to:</span></span>

* <span data-ttu-id="7a93c-194">**重新啟動主動控制器的 hello** – 您會收到通知，重新啟動主動控制器造成 hello 裝置 toofail 透過 toohello 被動控制站。</span><span class="sxs-lookup"><span data-stu-id="7a93c-194">**Restart hello active controller** – You are notified that restarting an active controller caused hello device toofail over toohello passive controller.</span></span> <span data-ttu-id="7a93c-195">hello 控制器會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="7a93c-195">hello controller restarts.</span></span>
* <span data-ttu-id="7a93c-196">**關閉主動控制器** – 您會收到通知，告知您關閉主動控制器將導致停機。</span><span class="sxs-lookup"><span data-stu-id="7a93c-196">**Shut down an active controller** – You are notified that shutting down an active controller results in downtime.</span></span> <span data-ttu-id="7a93c-197">您也需要 hello hello 控制站上的裝置 tooturn toopush hello 電源按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a93c-197">You also need toopush hello power button on hello device tooturn on hello controller.</span></span>

<span data-ttu-id="7a93c-198">**問：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-198">**Q.**</span></span> <span data-ttu-id="7a93c-199">如果我的裝置上的 hello 被動控制器無法使用或已關閉，因此我重新啟動或關閉 hello 主動控制器，則會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="7a93c-199">What happens if hello passive controller on my device is unavailable or turned off and I restart or shut down hello active controller?</span></span>

<span data-ttu-id="7a93c-200">**答：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-200">**A.**</span></span> <span data-ttu-id="7a93c-201">如果您的裝置上的 hello 被動控制器無法使用或已關閉，而且您選擇：</span><span class="sxs-lookup"><span data-stu-id="7a93c-201">If hello passive controller on your device is unavailable or turned off, and you choose to:</span></span>

* <span data-ttu-id="7a93c-202">**重新啟動主動控制器的 hello** – 繼續 hello 作業將會導致 hello 服務暫時中斷，系統會提示您確認您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="7a93c-202">**Restart hello active controller** – You are notified that continuing hello operation will result in a temporary disruption of hello service, and you are prompted for confirmation.</span></span>
* <span data-ttu-id="7a93c-203">**關閉主動控制器**– 就會通知您繼續 hello 作業會導致停機時間。</span><span class="sxs-lookup"><span data-stu-id="7a93c-203">**Shut down an active controller** – You are notified that continuing hello operation results in downtime.</span></span> <span data-ttu-id="7a93c-204">您也需要 hello 裝置上的一個或兩個控制器 tooturn toopush hello 電源按鈕。</span><span class="sxs-lookup"><span data-stu-id="7a93c-204">You also need toopush hello power button on one or both controllers tooturn on hello device.</span></span> <span data-ttu-id="7a93c-205">系統會提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="7a93c-205">You are prompted for confirmation.</span></span>

<span data-ttu-id="7a93c-206">**問：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-206">**Q.**</span></span> <span data-ttu-id="7a93c-207">何時沒有 hello 控制器重新啟動或關機失敗 tooprogress？</span><span class="sxs-lookup"><span data-stu-id="7a93c-207">When does hello controller restart or shutdown fails tooprogress?</span></span>

<span data-ttu-id="7a93c-208">**答：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-208">**A.**</span></span> <span data-ttu-id="7a93c-209">重新啟動或關閉控制器可能會在下列情況下失敗：</span><span class="sxs-lookup"><span data-stu-id="7a93c-209">Restarting or shutting down a controller may fail if:</span></span>

* <span data-ttu-id="7a93c-210">裝置更新進行中。</span><span class="sxs-lookup"><span data-stu-id="7a93c-210">A device update is in progress.</span></span>
* <span data-ttu-id="7a93c-211">控制器重新啟動已在進行中。</span><span class="sxs-lookup"><span data-stu-id="7a93c-211">A controller restart is already in progress.</span></span>
* <span data-ttu-id="7a93c-212">控制器關閉已在進行中。</span><span class="sxs-lookup"><span data-stu-id="7a93c-212">A controller shutdown is already in progress.</span></span>

<span data-ttu-id="7a93c-213">**問：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-213">**Q.**</span></span> <span data-ttu-id="7a93c-214">您如何判斷控制器已重新啟動或關閉？</span><span class="sxs-lookup"><span data-stu-id="7a93c-214">How can you figure out if a controller was restarted or shut down?</span></span>

<span data-ttu-id="7a93c-215">**答：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-215">**A.**</span></span> <span data-ttu-id="7a93c-216">您可以檢查 hello 控制器刀鋒視窗上的控制器狀態。</span><span class="sxs-lookup"><span data-stu-id="7a93c-216">You can check hello controller status on Controller blade.</span></span> <span data-ttu-id="7a93c-217">hello 控制器狀態會指出控制器是否在重新啟動或關閉 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="7a93c-217">hello controller status will indicate whether a controller is in hello process of restarting or shutting down.</span></span> <span data-ttu-id="7a93c-218">此外，hello**警示**刀鋒視窗包含資訊警示，如果 hello 控制站重新啟動或關機。</span><span class="sxs-lookup"><span data-stu-id="7a93c-218">Additionally, hello **Alerts** blade contain an informational alert if hello controller is restarted or shut down.</span></span> <span data-ttu-id="7a93c-219">hello 控制器重新啟動及關閉作業也會記錄在 hello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7a93c-219">hello controller restart and shutdown operations are also recorded in hello acitivity logs.</span></span> <span data-ttu-id="7a93c-220">如需活動記錄檔的詳細資訊，請移至太[檢視 hello 活動記錄檔](storsimple-8000-service-dashboard.md#view-the-activity-logs)。</span><span class="sxs-lookup"><span data-stu-id="7a93c-220">For more information about acitivity logs, go too[View hello activity logs](storsimple-8000-service-dashboard.md#view-the-activity-logs).</span></span>

<span data-ttu-id="7a93c-221">**問：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-221">**Q.**</span></span> <span data-ttu-id="7a93c-222">是否有任何影響 toohello I/O 控制器容錯移轉後？</span><span class="sxs-lookup"><span data-stu-id="7a93c-222">Is there any impact toohello I/O as a result of controller failover?</span></span>

<span data-ttu-id="7a93c-223">**答：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-223">**A.**</span></span> <span data-ttu-id="7a93c-224">由於控制器容錯移轉，將會重設 hello 啟動器與主動控制站之間的 TCP 連線，但 hello 被動控制器繼續作業時就會重新建立。</span><span class="sxs-lookup"><span data-stu-id="7a93c-224">hello TCP connections between initiators and active controller will be reset as a result of controller failover, but will be reestablished when hello passive controller assumes operation.</span></span> <span data-ttu-id="7a93c-225">Hello 課程的這項作業期間可能會暫時 （少於 30 秒） 暫停啟動器與 hello 裝置之間的 I/O 活動。</span><span class="sxs-lookup"><span data-stu-id="7a93c-225">There may be a temporary (less than 30 seconds) pause in I/O activity between initiators and hello device during hello course of this operation.</span></span>

<span data-ttu-id="7a93c-226">**問：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-226">**Q.**</span></span> <span data-ttu-id="7a93c-227">如何關閉和移除之後傳回我控制器 tooservice？</span><span class="sxs-lookup"><span data-stu-id="7a93c-227">How do I return my controller tooservice after it has been shut down and removed?</span></span>

<span data-ttu-id="7a93c-228">**答：**</span><span class="sxs-lookup"><span data-stu-id="7a93c-228">**A.**</span></span> <span data-ttu-id="7a93c-229">tooreturn 控制器 tooservice，您必須將它插入 hello 底座中所述[取代您的 StorSimple 裝置上的控制器模組](storsimple-8000-controller-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="7a93c-229">tooreturn a controller tooservice, you must insert it into hello chassis as described in [Replace a controller module on your StorSimple device](storsimple-8000-controller-replacement.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a93c-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a93c-230">Next steps</span></span>
* <span data-ttu-id="7a93c-231">如果您遇到任何問題，您無法使用此教學課程中所列的 hello 程序來解決您 StorSimple 裝置控制站與[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="7a93c-231">If you encounter any issues with your StorSimple device controllers that you cannot resolve by using hello procedures listed in this tutorial, [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="7a93c-232">toolearn 進一步了解使用 hello StorSimple 裝置管理員服務，請跳過[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="7a93c-232">toolearn more about using hello  StorSimple Device Manager service, go too[Use hello  StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

