---
title: "aaaManage StorSimple 裝置控制站 |Microsoft 文件"
description: "了解 toostop，重新啟動、 關機或重設您的 StorSimple 裝置控制站的方式。"
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
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a><span data-ttu-id="a4efd-103">管理 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="a4efd-103">Manage your StorSimple device controllers</span></span>
## <a name="overview"></a><span data-ttu-id="a4efd-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a4efd-104">Overview</span></span>
<span data-ttu-id="a4efd-105">本教學課程描述 hello 可在您的 StorSimple 裝置控制站執行的不同作業。</span><span class="sxs-lookup"><span data-stu-id="a4efd-105">This tutorial describes hello different operations that can be performed on your StorSimple device controllers.</span></span> <span data-ttu-id="a4efd-106">您的 StorSimple 裝置中的 hello 控制站會在主動-被動組態的備援 （對等） 控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-106">hello controllers in your StorSimple device are redundant (peer) controllers in an active-passive configuration.</span></span> <span data-ttu-id="a4efd-107">在指定的時間，只能有一個控制器為作用中，並處理所有的 hello 磁碟和網路作業。</span><span class="sxs-lookup"><span data-stu-id="a4efd-107">At a given time, only one controller is active and is processing all hello disk and network operations.</span></span> <span data-ttu-id="a4efd-108">hello 另一個控制器處於被動模式。</span><span class="sxs-lookup"><span data-stu-id="a4efd-108">hello other controller is in a passive mode.</span></span> <span data-ttu-id="a4efd-109">Hello 主動控制器失效，如果 hello 被動控制器會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="a4efd-109">If hello active controller fails, hello passive controller becomes active automatically.</span></span>

<span data-ttu-id="a4efd-110">本教學課程使用包含 toomanage hello 裝置控制站的逐步指示:</span><span class="sxs-lookup"><span data-stu-id="a4efd-110">This tutorial includes step-by-step instructions toomanage hello device controllers by using the:</span></span>

* <span data-ttu-id="a4efd-111">**控制站**區段 hello**維護**hello StorSimple Manager 服務中的頁面</span><span class="sxs-lookup"><span data-stu-id="a4efd-111">**Controllers** section of hello **Maintenance** page in hello StorSimple Manager service</span></span>
* <span data-ttu-id="a4efd-112">Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="a4efd-112">Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="a4efd-113">我們建議您管理透過 hello StorSimple Manager 服務的 hello 裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-113">We recommend that you manage hello device controllers via hello StorSimple Manager service.</span></span> <span data-ttu-id="a4efd-114">如果只可以使用 Windows PowerShell for StorSimple 執行某個動作，hello 教學課程還會記錄下來。</span><span class="sxs-lookup"><span data-stu-id="a4efd-114">If an action can only be performed by using Windows PowerShell for StorSimple, hello tutorial makes a note of it.</span></span>

<span data-ttu-id="a4efd-115">閱讀本教學課程之後，您將能夠：</span><span class="sxs-lookup"><span data-stu-id="a4efd-115">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="a4efd-116">重新啟動或關閉 StorSimple 裝置控制器</span><span class="sxs-lookup"><span data-stu-id="a4efd-116">Restart or shut down a StorSimple device controller</span></span>
* <span data-ttu-id="a4efd-117">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="a4efd-117">Shut down a StorSimple device</span></span>
* <span data-ttu-id="a4efd-118">重設您的 StorSimple 裝置 toofactory 預設值</span><span class="sxs-lookup"><span data-stu-id="a4efd-118">Reset your StorSimple device toofactory defaults</span></span>

## <a name="restart-or-shut-down-a-single-controller"></a><span data-ttu-id="a4efd-119">重新啟動或關閉單一控制器</span><span class="sxs-lookup"><span data-stu-id="a4efd-119">Restart or shut down a single controller</span></span>
<span data-ttu-id="a4efd-120">一般系統作業並不需要重新啟動或關閉控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-120">A controller restart or shutdown is not required as a part of normal system operation.</span></span> <span data-ttu-id="a4efd-121">只有在故障的裝置硬體元件需要更換時，才會常常使用單一裝置控制器的關閉作業。</span><span class="sxs-lookup"><span data-stu-id="a4efd-121">Shutdown operations for a single device controller are common only in cases in which a failed device hardware component requires replacement.</span></span> <span data-ttu-id="a4efd-122">只有在記憶體過度使用或控制器故障影響效能時，才會需要重新啟動控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-122">A controller restart may also be required in a situation in which performance is affected by excessive memory usage or a malfunctioning controller.</span></span> <span data-ttu-id="a4efd-123">您也可能需要 toorestart 控制站之後在成功更換控制器，如果您希望 tooenable 測試 hello 取代控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-123">You may also need toorestart a controller after a successful controller replacement, if you wish tooenable and test hello replaced controller.</span></span>

<span data-ttu-id="a4efd-124">重新啟動的裝置不干擾 tooconnected 啟動器，假設 hello 被動控制站可用。</span><span class="sxs-lookup"><span data-stu-id="a4efd-124">Restarting a device is not disruptive tooconnected initiators, assuming hello passive controller is available.</span></span> <span data-ttu-id="a4efd-125">如果是被動控制器無法使用或已關閉，然後重新啟動 hello active 控制器可能會導致 hello 服務中斷和停機時間。</span><span class="sxs-lookup"><span data-stu-id="a4efd-125">If a passive controller is not available or turned off, then restarting hello active controller may result in hello disruption of service and downtime.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="a4efd-126">**執行中的控制器應該永遠不會實際移除，因為這會導致失去備援並增加停機的風險。**</span><span class="sxs-lookup"><span data-stu-id="a4efd-126">**A running controller should never be physically removed as this would result in a loss of redundancy and an increased risk of downtime.**</span></span>
> * <span data-ttu-id="a4efd-127">hello 下列程序適用於僅 toohello StorSimple 實體裝置。</span><span class="sxs-lookup"><span data-stu-id="a4efd-127">hello following procedure applies only toohello StorSimple physical device.</span></span> <span data-ttu-id="a4efd-128">如需有關如何 toostart、 停止及重新啟動 hello 虛擬裝置，請參閱資訊[與 hello 虛擬裝置搭配使用](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-128">For information about how toostart, stop, and restart hello virtual device, see [Work with hello virtual device](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device).</span></span>
> 
> 

<span data-ttu-id="a4efd-129">您可以重新啟動或關機的單一裝置控制站使用 for StorSimple 的 hello hello StorSimple Manager 服務或 Windows PowerShell 的 Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a4efd-129">You can restart or shut down a single device controller by using hello Azure classic portal of hello StorSimple Manager service or Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="a4efd-130">toomanage hello Azure 傳統入口網站，從您的裝置控制站執行下列步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="a4efd-130">toomanage your device controllers from hello Azure classic portal, perform hello following steps.</span></span>

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a><span data-ttu-id="a4efd-131">toorestart 或傳統入口網站中的控制站關機</span><span class="sxs-lookup"><span data-stu-id="a4efd-131">toorestart or shut down a controller in classic portal</span></span>
1. <span data-ttu-id="a4efd-132">瀏覽過**裝置 > 維護**。</span><span class="sxs-lookup"><span data-stu-id="a4efd-132">Navigate too**Devices > Maintenance**.</span></span>
2. <span data-ttu-id="a4efd-133">跳過**硬體狀態**，並確認您的裝置上的兩個 hello 控制器 hello 狀態**狀況良好**。</span><span class="sxs-lookup"><span data-stu-id="a4efd-133">Go too**Hardware Status** and verify that hello status of both hello controllers on your device is **Healthy**.</span></span>
   
    ![確認 StorSimple 裝置控制器的狀況良好](./media/storsimple-manage-device-controller/IC766017.png)
3. <span data-ttu-id="a4efd-135">從 hello 底部 hello**維護**頁面上，按一下**管理控制器**。</span><span class="sxs-lookup"><span data-stu-id="a4efd-135">From hello bottom of hello **Maintenance** page, click **Manage Controllers**.</span></span>
   
    ![管理 StorSimple 裝置控制器](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > <span data-ttu-id="a4efd-137">如果您看**管理控制器**，則您需要 tooinstall 更新。</span><span class="sxs-lookup"><span data-stu-id="a4efd-137">If you cannot see **Manage Controllers**, then you need tooinstall updates.</span></span> <span data-ttu-id="a4efd-138">如需詳細資訊，請參閱 [更新您的 StorSimple 裝置](storsimple-update-device.md)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-138">For more information, see [Update your StorSimple device](storsimple-update-device.md).</span></span>
   > 
   > 
4. <span data-ttu-id="a4efd-139">在 hello**變更控制器設定**對話方塊方塊中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a4efd-139">In hello **Change Controller Settings** dialog box, do hello following:</span></span>
   
   1. <span data-ttu-id="a4efd-140">從 hello**選取控制器**下拉式清單中，您想 toomanage 選取 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="a4efd-140">From hello **Select Controller** drop-down list, select hello controller that you want toomanage.</span></span> <span data-ttu-id="a4efd-141">hello 選項為控制器 0 及控制器 1。</span><span class="sxs-lookup"><span data-stu-id="a4efd-141">hello options are Controller 0 and Controller 1.</span></span> <span data-ttu-id="a4efd-142">這些控制器也可識別為主動或被動。</span><span class="sxs-lookup"><span data-stu-id="a4efd-142">These controllers are also identified as active or passive.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a4efd-143">控制器無法使用，便無法使用或已關閉，而且它不會出現在 hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="a4efd-143">A controller cannot be managed if it is unavailable or turned off, and it will not appear in hello drop-down list.</span></span>
      > 
      > 
   2. <span data-ttu-id="a4efd-144">從 hello**選取動作**下拉式清單中，選擇**重新啟動控制器**或**關閉控制器**。</span><span class="sxs-lookup"><span data-stu-id="a4efd-144">From hello **Select Action** drop-down list, choose **Restart controller** or **Shut down controller**.</span></span>
      
       ![重新啟動 StorSimple 裝置被動控制器](./media/storsimple-manage-device-controller/IC766020.png)
   3. <span data-ttu-id="a4efd-146">按一下 [hello] 核取圖示</span><span class="sxs-lookup"><span data-stu-id="a4efd-146">Click hello check icon</span></span> ![核取圖示](./media/storsimple-manage-device-controller/IC740895.png)<span data-ttu-id="a4efd-148">.</span><span class="sxs-lookup"><span data-stu-id="a4efd-148">.</span></span>

<span data-ttu-id="a4efd-149">這將會重新啟動或關閉 hello 控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-149">This will restart or shut down hello controller.</span></span> <span data-ttu-id="a4efd-150">hello 下表摘要說明 hello 詳細資料，根據您 hello 中所做的 hello 選項發生什麼事**變更控制器設定** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="a4efd-150">hello table below summarizes hello details of what happens depending on hello selections you have made in hello **Change Controller Settings** dialog box.</span></span>  

| <span data-ttu-id="a4efd-151">選取項目 #</span><span class="sxs-lookup"><span data-stu-id="a4efd-151">Selection #</span></span> | <span data-ttu-id="a4efd-152">如果您選擇...</span><span class="sxs-lookup"><span data-stu-id="a4efd-152">If you choose to...</span></span> | <span data-ttu-id="a4efd-153">就會發生這個狀況。</span><span class="sxs-lookup"><span data-stu-id="a4efd-153">This will happen.</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4efd-154">1.</span><span class="sxs-lookup"><span data-stu-id="a4efd-154">1.</span></span> |<span data-ttu-id="a4efd-155">重新啟動 hello 被動控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-155">Restart hello passive controller.</span></span> |<span data-ttu-id="a4efd-156">Toorestart hello 控制站，將會建立一個作業，且 hello 工作成功建立後將會通知您。</span><span class="sxs-lookup"><span data-stu-id="a4efd-156">A job will be created toorestart hello controller, and you will be notified after hello job is successfully created.</span></span> <span data-ttu-id="a4efd-157">這會起始 hello 控制器重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a4efd-157">This will initiate hello controller restart.</span></span> <span data-ttu-id="a4efd-158">您可以藉由存取監視 hello 重新啟動程序**服務 > 儀表板 > 檢視作業記錄檔**然後篩選參數特定 tooyour 服務。</span><span class="sxs-lookup"><span data-stu-id="a4efd-158">You can monitor hello restart process by accessing **Service > Dashboard > View operation logs** and then filtering by parameters specific tooyour service.</span></span> |
| <span data-ttu-id="a4efd-159">2.</span><span class="sxs-lookup"><span data-stu-id="a4efd-159">2.</span></span> |<span data-ttu-id="a4efd-160">重新啟動 hello 作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-160">Restart hello active controller.</span></span> |<span data-ttu-id="a4efd-161">您會看到下列警告 hello: 「 如果您重新啟動 hello 作用中控制器，hello 裝置將無法透過 toohello 被動控制站。</span><span class="sxs-lookup"><span data-stu-id="a4efd-161">You will see hello following warning: "If you restart hello active controller, hello device will fail over toohello passive controller.</span></span> <span data-ttu-id="a4efd-162">您想 toocontinue？ 」</span><span class="sxs-lookup"><span data-stu-id="a4efd-162">Do you want toocontinue?"</span></span> </br><span data-ttu-id="a4efd-163">如果您選擇 tooproceed 進行這項作業，hello 下一個步驟將會使用相同 toothose toorestart hello 被動控制站 （請參閱選取項目 1）。</span><span class="sxs-lookup"><span data-stu-id="a4efd-163">If you choose tooproceed with this operation, hello next steps will be identical toothose used toorestart hello passive controller (see selection 1).</span></span> |
| <span data-ttu-id="a4efd-164">3.</span><span class="sxs-lookup"><span data-stu-id="a4efd-164">3.</span></span> |<span data-ttu-id="a4efd-165">Hello 被動控制站關機。</span><span class="sxs-lookup"><span data-stu-id="a4efd-165">Shut down hello passive controller.</span></span> |<span data-ttu-id="a4efd-166">您會看到下列訊息的 hello: 「 關閉已完成之後，您將需要 toopush hello 電源按鈕上控制器 tooturn 它。</span><span class="sxs-lookup"><span data-stu-id="a4efd-166">You will see hello following message: "After shutdown is complete, you will need toopush hello power button on your controller tooturn it on.</span></span> <span data-ttu-id="a4efd-167">確定要關閉此控制站 tooshut？ 」</span><span class="sxs-lookup"><span data-stu-id="a4efd-167">Are you sure you want tooshut down this controller?"</span></span> </br><span data-ttu-id="a4efd-168">如果您選擇 tooproceed 進行這項作業，hello 下一個步驟將會使用相同 toothose toorestart hello 被動控制站 （請參閱選取項目 1）。</span><span class="sxs-lookup"><span data-stu-id="a4efd-168">If you choose tooproceed with this operation, hello next steps will be identical toothose used toorestart hello passive controller (see selection 1).</span></span> |
| <span data-ttu-id="a4efd-169">4.</span><span class="sxs-lookup"><span data-stu-id="a4efd-169">4.</span></span> |<span data-ttu-id="a4efd-170">關閉 hello 作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-170">Shut down hello active controller.</span></span> |<span data-ttu-id="a4efd-171">您會看到下列訊息的 hello: 「 關閉已完成之後，您將需要 toopush hello 電源按鈕上控制器 tooturn 它。</span><span class="sxs-lookup"><span data-stu-id="a4efd-171">You will see hello following message: "After shutdown is complete, you will need toopush hello power button on your controller tooturn it on.</span></span> <span data-ttu-id="a4efd-172">確定要關閉此控制站 tooshut？ 」</span><span class="sxs-lookup"><span data-stu-id="a4efd-172">Are you sure you want tooshut down this controller?"</span></span> </br><span data-ttu-id="a4efd-173">如果您選擇 tooproceed 進行這項作業，hello 下一個步驟將會使用相同 toothose toorestart hello 被動控制站 （請參閱選取項目 1）。</span><span class="sxs-lookup"><span data-stu-id="a4efd-173">If you choose tooproceed with this operation, hello next steps will be identical toothose used toorestart hello passive controller (see selection 1).</span></span> |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a4efd-174">toorestart 或關機的控制站，在 Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="a4efd-174">toorestart or shut down a controller in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="a4efd-175">執行 hello 遵循步驟 tooshut 關閉或重新啟動 StorSimple 裝置 hello Azure 傳統入口網站從單一控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-175">Perform hello following steps tooshut down or restart a single controller on your StorSimple device from hello Azure classic portal.</span></span>

1. <span data-ttu-id="a4efd-176">使用 hello 序列主控台或 telnet 工作階段從遠端電腦存取 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="a4efd-176">Access hello device by using hello serial console or a telnet session from a remote computer.</span></span> <span data-ttu-id="a4efd-177">連線 tooController 0 或控制器 1，由下列 hello 中的步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-177">Connect tooController 0 or Controller 1 by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="a4efd-178">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="a4efd-178">In hello serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="a4efd-179">在 hello 橫幅訊息中，記下過，您所連接的 hello 控制器 （控制器 0 或控制器 1），以及是否使用中的 hello 被動 （待命） 控制站。</span><span class="sxs-lookup"><span data-stu-id="a4efd-179">In hello banner message, make a note of hello controller you are connected too(Controller 0 or Controller 1) and whether it is hello active or hello passive (standby) controller.</span></span>
   
   * <span data-ttu-id="a4efd-180">tooshut 關閉單一控制器，在 hello 提示字元，輸入：</span><span class="sxs-lookup"><span data-stu-id="a4efd-180">tooshut down a single controller, at hello prompt, type:</span></span>
     
       `Stop-HcsController`
     
       <span data-ttu-id="a4efd-181">這將會關閉您所連接的 hello 控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-181">This will shut down hello controller that you are connected to.</span></span> <span data-ttu-id="a4efd-182">如果您停止 hello 作用中控制器，然後它將會容錯移轉 toohello 被動控制器在關閉之前。</span><span class="sxs-lookup"><span data-stu-id="a4efd-182">If you stop hello active controller, then it will fail over toohello passive controller before it shuts down.</span></span>
   * <span data-ttu-id="a4efd-183">toorestart 控制站，在 hello 提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="a4efd-183">toorestart a controller, at hello prompt, type:</span></span>
     
       `Restart-HcsController`
     
       <span data-ttu-id="a4efd-184">這會重新啟動您所連接的 hello 控制站。</span><span class="sxs-lookup"><span data-stu-id="a4efd-184">This will restart hello controller that you are connected to.</span></span> <span data-ttu-id="a4efd-185">如果您重新啟動 hello 作用中控制器，它將容錯移轉 toohello 被動控制站之前 hello 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a4efd-185">If you restart hello active controller, it will fail over toohello passive controller before hello restart.</span></span>

## <a name="shut-down-a-storsimple-device"></a><span data-ttu-id="a4efd-186">關閉 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="a4efd-186">Shut down a StorSimple device</span></span>
<span data-ttu-id="a4efd-187">本章節將說明如何 tooshut 關閉執行中或失敗的 StorSimple 裝置，從遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="a4efd-187">This section explains how tooshut down a running or a failed StorSimple device from a remote computer.</span></span> <span data-ttu-id="a4efd-188">裝置已關閉之後關閉兩個 hello 裝置控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-188">A device is turned off after shutting down both hello device controllers.</span></span> <span data-ttu-id="a4efd-189">Hello 裝置實際移動，或帶離服務時，是完成裝置關機。</span><span class="sxs-lookup"><span data-stu-id="a4efd-189">A device shutdown is done when hello device is being physically moved, or is taken out of service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4efd-190">您關閉 hello 裝置之前，請檢查 hello hello 裝置元件健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a4efd-190">Before you shut down hello device, check hello health of hello device components.</span></span> <span data-ttu-id="a4efd-191">瀏覽過**裝置 > 維護 > 硬體狀態**並確認所有 hello 元件 hello LED 狀態為綠色。</span><span class="sxs-lookup"><span data-stu-id="a4efd-191">Navigate too**Devices > Maintenance > Hardware Status** and verify that hello LED status of all hello components is green.</span></span> <span data-ttu-id="a4efd-192">只有狀況良好的裝置才會有綠色的狀態。</span><span class="sxs-lookup"><span data-stu-id="a4efd-192">Only a healthy device will have a green status.</span></span> <span data-ttu-id="a4efd-193">如果您的裝置關機 tooreplace 的故障元件時，您會看到故障 （紅色） 或降級 （黃色） 狀態 hello 個別元件。</span><span class="sxs-lookup"><span data-stu-id="a4efd-193">If your device is being shut down tooreplace a malfunctioning component, you will see a failed (red) or a degraded (yellow) status for hello respective component(s).</span></span>
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a><span data-ttu-id="a4efd-194">tooshut StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="a4efd-194">tooshut down a StorSimple device</span></span>
1. <span data-ttu-id="a4efd-195">使用 hello[重新啟動或關閉控制器](#restart-or-shut-down-a-single-controller)程序 tooidentify 並關機 hello 裝置上的被動控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-195">Use hello [restart or shut down a controller](#restart-or-shut-down-a-single-controller) procedure tooidentify and shut down hello passive controller on your device.</span></span> <span data-ttu-id="a4efd-196">您可以針對 StorSimple hello Azure 傳統入口網站或 Windows PowerShell 中執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="a4efd-196">You can perform this operation in hello Azure classic portal or in Windows PowerShell for StorSimple.</span></span>
2. <span data-ttu-id="a4efd-197">重複上述步驟 tooshut 向 hello 作用中控制器的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4efd-197">Repeat hello above step tooshut down hello active controller.</span></span>
3. <span data-ttu-id="a4efd-198">您現在就必須在 hello toolook 背 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="a4efd-198">You will now need toolook at hello back plane of hello device.</span></span> <span data-ttu-id="a4efd-199">Hello 兩個控制器都關閉之後，hello 兩個 hello 控制器狀態 Led 應閃爍紅燈。</span><span class="sxs-lookup"><span data-stu-id="a4efd-199">After hello two controllers are completely shut down, hello status LEDs on both hello controllers should be blinking red.</span></span> <span data-ttu-id="a4efd-200">如果您完全在這個階段需要關閉裝置 hello tooturn 上電源和冷卻模組 (Pcm), 翻轉 hello 電源開關 toohello OFF 位置。</span><span class="sxs-lookup"><span data-stu-id="a4efd-200">If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.</span></span> <span data-ttu-id="a4efd-201">這應該關閉 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="a4efd-201">This should turn off hello device.</span></span>

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a><span data-ttu-id="a4efd-202">重設 hello 裝置 toofactory 預設值</span><span class="sxs-lookup"><span data-stu-id="a4efd-202">Reset hello device toofactory default settings</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a4efd-203">如果您需要 tooreset 裝置 toofactory 預設設定，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="a4efd-203">If you need tooreset your device toofactory default settings, contact Microsoft Support.</span></span> <span data-ttu-id="a4efd-204">hello 如下所述的程序只應該用於搭配 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="a4efd-204">hello procedure described below should be used only in conjunction with Microsoft Support.</span></span>
> 
> 

<span data-ttu-id="a4efd-205">此程序描述如何 tooreset 您 Microsoft Azure StorSimple 裝置 toofactory 的預設設定使用 Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="a4efd-205">This procedure describes how tooreset your Microsoft Azure StorSimple device toofactory default settings using Windows PowerShell for StorSimple.</span></span>
<span data-ttu-id="a4efd-206">重設裝置移除所有資料和設定預設的 hello 整個叢集。</span><span class="sxs-lookup"><span data-stu-id="a4efd-206">Resetting a device removes all data and settings from hello entire cluster by default.</span></span>

<span data-ttu-id="a4efd-207">您的 Microsoft Azure StorSimple 裝置 toofactory 預設設定執行下列步驟 tooreset hello:</span><span class="sxs-lookup"><span data-stu-id="a4efd-207">Perform hello following steps tooreset your Microsoft Azure StorSimple device toofactory default settings:</span></span>

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a><span data-ttu-id="a4efd-208">tooreset hello toodefault 的裝置設定 Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="a4efd-208">tooreset hello device toodefault settings in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="a4efd-209">透過序列主控台存取 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="a4efd-209">Access hello device through its serial console.</span></span> <span data-ttu-id="a4efd-210">請檢查您是連接的 toohello 作用中控制器的 hello 橫幅訊息 tooensure。</span><span class="sxs-lookup"><span data-stu-id="a4efd-210">Check hello banner message tooensure that you are connected toohello Active controller.</span></span>
2. <span data-ttu-id="a4efd-211">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="a4efd-211">In hello serial console menu, choose option 1, **Log in with full access**.</span></span>
3. <span data-ttu-id="a4efd-212">在 hello 提示中輸入下列命令 tooreset hello 整個叢集，移除所有的資料、 中繼資料及控制器設定 hello:</span><span class="sxs-lookup"><span data-stu-id="a4efd-212">At hello prompt, type hello following command tooreset hello entire cluster, removing all data, metadata, and controller settings:</span></span>
   
    `Reset-HcsFactoryDefault`
   
    <span data-ttu-id="a4efd-213">tooinstead 重設一個控制器，請使用 hello [Reset-hcsfactorydefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet 搭配 hello`-scope`參數。)</span><span class="sxs-lookup"><span data-stu-id="a4efd-213">tooinstead reset a single controller, use hello  [Reset-HcsFactoryDefault](http://technet.microsoft.com/library/dn688132.aspx) cmdlet with hello `-scope` parameter.)</span></span>
   
    <span data-ttu-id="a4efd-214">hello 系統將會重新啟動多次。</span><span class="sxs-lookup"><span data-stu-id="a4efd-214">hello system will reboot multiple times.</span></span> <span data-ttu-id="a4efd-215">Hello 重設已順利完成時，系統會通知您。</span><span class="sxs-lookup"><span data-stu-id="a4efd-215">You will be notified when hello reset has successfully completed.</span></span> <span data-ttu-id="a4efd-216">根據 hello 系統模型，它可能需要 45-60 分鐘 8100 裝置和 60-90 分鐘的 8600 toofinish 此程序。</span><span class="sxs-lookup"><span data-stu-id="a4efd-216">Depending on hello system model, it can take 45-60 minutes for an 8100 device and 60-90 minutes for an 8600 toofinish this process.</span></span>
   
   > [!TIP]
   > * <span data-ttu-id="a4efd-217">如果您使用更新 1.2 或是之前使用 hello`–SkipFirmwareVersionCheck`參數 tooskip hello 韌體版本檢查 (否則，您會看到韌體不符錯誤： 無法繼續原廠重設，因為 tooa hello 韌體版本不符。</span><span class="sxs-lookup"><span data-stu-id="a4efd-217">If you're using Update 1.2 or earlier use hello `–SkipFirmwareVersionCheck` parameter tooskip hello firmware version check (otherwise you'll see a firmware mismatch error: Factory reset cannot continue due tooa mismatch in hello firmware versions.</span></span> <span data-ttu-id="a4efd-218">)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-218">).</span></span>
   > * <span data-ttu-id="a4efd-219">正在更新 1 或 1.1 hello 政府入口網站中，且已執行成功的單一或雙重控制器更換 （與 Update 1 所隨附的替換控制器的 StorSimple 裝置 hello 原廠重設程序可能會失敗軟體）。</span><span class="sxs-lookup"><span data-stu-id="a4efd-219">hello factory reset procedure may fail for StorSimple devices that are running Update 1 or 1.1 in hello Government portal and have performed a successful single or dual controller replacement (with replacement controllers that were shipped with pre-Update 1 software).</span></span> <span data-ttu-id="a4efd-220">發生這種情況時 hello 原廠重設映像驗證 hello SHA1 檔案不存在的 hello 控制站上的更新前 1 軟體存在。</span><span class="sxs-lookup"><span data-stu-id="a4efd-220">This happens when hello factory reset image is validated for hello presence of a SHA1 file on hello controller that does not exist for pre-Update 1 software.</span></span> <span data-ttu-id="a4efd-221">如果您看到此原廠重設失敗，請連絡 Microsoft 支援服務 tooassist 您 hello 與後續步驟。</span><span class="sxs-lookup"><span data-stu-id="a4efd-221">If you see this factory reset failure, contact Microsoft Support tooassist you with hello next steps.</span></span> <span data-ttu-id="a4efd-222">此問題不會出現與出貨從更新 1 或更新版本的軟體 hello 原廠替換控制器。</span><span class="sxs-lookup"><span data-stu-id="a4efd-222">This issue is not seen with replacement controllers that were shipped from hello factory with Update 1 or later software.</span></span>
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a><span data-ttu-id="a4efd-223">有關管理裝置控制器的問題與解答</span><span class="sxs-lookup"><span data-stu-id="a4efd-223">Questions and answers about managing device controllers</span></span>
<span data-ttu-id="a4efd-224">在本節中，我們有摘要一些 hello 常見問題集有關管理 StorSimple 裝置控制站。</span><span class="sxs-lookup"><span data-stu-id="a4efd-224">In this section, we have summarized some of hello frequently asked questions regarding managing StorSimple device controllers.</span></span>

<span data-ttu-id="a4efd-225">**問：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-225">**Q.**</span></span> <span data-ttu-id="a4efd-226">如果兩者 hello 我的裝置上控制站，會發生什麼情況都是狀況良好並已在與我重新啟動或關閉 hello 主動控制器？</span><span class="sxs-lookup"><span data-stu-id="a4efd-226">What happens if both hello controllers on my device are healthy and turned on and I restart or shut down hello active controller?</span></span>

<span data-ttu-id="a4efd-227">**答：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-227">**A.**</span></span> <span data-ttu-id="a4efd-228">如果您的裝置上的兩個 hello 控制器皆狀況良好並已 on 時，系統會提示您確認。</span><span class="sxs-lookup"><span data-stu-id="a4efd-228">If both hello controllers on your device are healthy and turned on, you will be prompted for confirmation.</span></span> <span data-ttu-id="a4efd-229">您可以選擇：</span><span class="sxs-lookup"><span data-stu-id="a4efd-229">You may choose to:</span></span>

* <span data-ttu-id="a4efd-230">**重新啟動主動控制器的 hello** – 您將會收到通知，重新啟動主動控制器將會導致 hello 裝置 toofail 透過 toohello 被動控制站。</span><span class="sxs-lookup"><span data-stu-id="a4efd-230">**Restart hello active controller** – You will be notified that restarting an active controller will cause hello device toofail over toohello passive controller.</span></span> <span data-ttu-id="a4efd-231">hello 控制器將會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a4efd-231">hello controller will restart.</span></span>
* <span data-ttu-id="a4efd-232">**關閉主動控制器** – 您將會收到通知，告知您關閉主動控制器將導致停機。</span><span class="sxs-lookup"><span data-stu-id="a4efd-232">**Shut down an active controller** – You will be notified that shutting down an active controller will result in downtime.</span></span> <span data-ttu-id="a4efd-233">您也必須上 hello hello 控制站上的裝置 tooturn toopush hello 電源 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4efd-233">You will also need toopush hello power button on hello device tooturn on hello controller.</span></span>

<span data-ttu-id="a4efd-234">**問：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-234">**Q.**</span></span> <span data-ttu-id="a4efd-235">如果我的裝置上的 hello 被動控制器無法使用或已關閉，因此我重新啟動或關閉 hello 主動控制器，則會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="a4efd-235">What happens if hello passive controller on my device is unavailable or turned off and I restart or shut down hello active controller?</span></span>

<span data-ttu-id="a4efd-236">**答：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-236">**A.**</span></span> <span data-ttu-id="a4efd-237">如果您的裝置上的 hello 被動控制器無法使用或已關閉，而且您選擇：</span><span class="sxs-lookup"><span data-stu-id="a4efd-237">If hello passive controller on your device is unavailable or turned off, and you choose to:</span></span>

* <span data-ttu-id="a4efd-238">**重新啟動主動控制器的 hello** – 系統會通知您繼續 hello 作業將會導致 hello 服務暫時中斷，系統將提示您確認。</span><span class="sxs-lookup"><span data-stu-id="a4efd-238">**Restart hello active controller** – You will be notified that continuing hello operation will result in a temporary disruption of hello service, and you will be prompted for confirmation.</span></span>
* <span data-ttu-id="a4efd-239">**關閉主動控制器**– 系統會通知您，繼續 hello 作業將導致停機時間，而且您必須在 hello 裝置上的一個或兩個控制器 tooturn toopush hello 電源 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a4efd-239">**Shut down an active controller** – You will be notified that continuing hello operation will result in downtime, and that you will need toopush hello power button on one or both controllers tooturn on hello device.</span></span> <span data-ttu-id="a4efd-240">系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="a4efd-240">You will be prompted for confirmation.</span></span>

<span data-ttu-id="a4efd-241">**問：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-241">**Q.**</span></span> <span data-ttu-id="a4efd-242">何時沒有 hello 控制器重新啟動或關機失敗 tooprogress？</span><span class="sxs-lookup"><span data-stu-id="a4efd-242">When does hello controller restart or shutdown fails tooprogress?</span></span>

<span data-ttu-id="a4efd-243">**答：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-243">**A.**</span></span> <span data-ttu-id="a4efd-244">重新啟動或關閉控制器可能會在下列情況下失敗：</span><span class="sxs-lookup"><span data-stu-id="a4efd-244">Restarting or shutting down a controller may fail if:</span></span>

* <span data-ttu-id="a4efd-245">裝置更新進行中。</span><span class="sxs-lookup"><span data-stu-id="a4efd-245">A device update is in progress.</span></span>
* <span data-ttu-id="a4efd-246">控制器重新啟動已在進行中。</span><span class="sxs-lookup"><span data-stu-id="a4efd-246">A controller restart is already in progress.</span></span>
* <span data-ttu-id="a4efd-247">控制器關閉已在進行中。</span><span class="sxs-lookup"><span data-stu-id="a4efd-247">A controller shutdown is already in progress.</span></span>

<span data-ttu-id="a4efd-248">**問：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-248">**Q.**</span></span> <span data-ttu-id="a4efd-249">您如何判斷控制器已重新啟動或關閉？</span><span class="sxs-lookup"><span data-stu-id="a4efd-249">How can you figure out if a controller was restarted or shut down?</span></span>

<span data-ttu-id="a4efd-250">**答：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-250">**A.**</span></span> <span data-ttu-id="a4efd-251">您可以檢查 hello hello 維護 頁面上的控制器狀態。</span><span class="sxs-lookup"><span data-stu-id="a4efd-251">You can check hello controller status on hello Maintenance page.</span></span> <span data-ttu-id="a4efd-252">hello 控制器狀態會指出控制器是否已重新啟動或關機。</span><span class="sxs-lookup"><span data-stu-id="a4efd-252">hello controller status will indicate whether a controller has been restarted or shut down.</span></span> <span data-ttu-id="a4efd-253">此外，如果 hello 控制器重新啟動或關閉 hello 警示 頁面會包含資訊警示。</span><span class="sxs-lookup"><span data-stu-id="a4efd-253">Additionally, hello Alerts page will contain an informational alert if hello controller was restarted or shut down.</span></span> <span data-ttu-id="a4efd-254">hello 控制器重新啟動及關閉作業也會記錄在 hello 作業記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a4efd-254">hello controller restart and shutdown operations are also recorded in hello operation logs.</span></span> <span data-ttu-id="a4efd-255">如需作業記錄檔的詳細資訊，請移至太[檢視 hello 作業記錄檔](storsimple-service-dashboard.md#view-the-operations-logs)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-255">For more information about operation logs, go too[View hello operation logs](storsimple-service-dashboard.md#view-the-operations-logs).</span></span>

<span data-ttu-id="a4efd-256">**問：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-256">**Q.**</span></span> <span data-ttu-id="a4efd-257">是否有任何影響 toohello I/o 控制器容錯移轉後？</span><span class="sxs-lookup"><span data-stu-id="a4efd-257">Is there any impact toohello I/Os as a result of controller failover?</span></span>

<span data-ttu-id="a4efd-258">**答：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-258">**A.**</span></span> <span data-ttu-id="a4efd-259">由於控制器容錯移轉，將會重設 hello 啟動器與主動控制站之間的 TCP 連線，但 hello 被動控制器繼續作業時就會重新建立。</span><span class="sxs-lookup"><span data-stu-id="a4efd-259">hello TCP connections between initiators and active controller will be reset as a result of controller failover, but will be reestablished when hello passive controller assumes operation.</span></span> <span data-ttu-id="a4efd-260">Hello 課程的這項作業期間可能會暫時 （少於 30 秒） 暫停啟動器與 hello 裝置之間的 I/O 活動。</span><span class="sxs-lookup"><span data-stu-id="a4efd-260">There may be a temporary (less than 30 seconds) pause in I/O activity between initiators and hello device during hello course of this operation.</span></span>

<span data-ttu-id="a4efd-261">**問：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-261">**Q.**</span></span> <span data-ttu-id="a4efd-262">如何關閉和移除之後傳回我控制器 tooservice？</span><span class="sxs-lookup"><span data-stu-id="a4efd-262">How do I return my controller tooservice after it has been shut down and removed?</span></span>

<span data-ttu-id="a4efd-263">**答：**</span><span class="sxs-lookup"><span data-stu-id="a4efd-263">**A.**</span></span> <span data-ttu-id="a4efd-264">tooreturn 控制器 tooservice，您必須將它插入 hello 底座中所述[取代您的 StorSimple 裝置上的控制器模組](storsimple-controller-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-264">tooreturn a controller tooservice, you must insert it into hello chassis as described in [Replace a controller module on your StorSimple device](storsimple-controller-replacement.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4efd-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4efd-265">Next steps</span></span>
* <span data-ttu-id="a4efd-266">如果您遇到任何問題，您無法使用此教學課程中所列的 hello 程序來解決您 StorSimple 裝置控制站與[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-266">If you encounter any issues with your StorSimple device controllers that you cannot resolve by using hello procedures listed in this tutorial, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="a4efd-267">toolearn 進一步了解使用 hello StorSimple Manager 服務，請跳過[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="a4efd-267">toolearn more about using hello StorSimple Manager service, go too[Use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

