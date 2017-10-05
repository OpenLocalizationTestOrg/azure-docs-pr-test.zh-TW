---
title: "變更 StorSimple 裝置模式 | Microsoft Docs"
description: "描述 StorSimple 裝置模式並說明如何使用 Windows PowerShell for StorSimple 來變更裝置的模式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="5bac1-103">變更 StorSimple 裝置的裝置模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="5bac1-104">本文提供 StorSimple 裝置各種運作模式的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="5bac1-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="5bac1-105">StorSimple 裝置有三種運作模式：標準、維護和復原。</span><span class="sxs-lookup"><span data-stu-id="5bac1-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="5bac1-106">閱讀本文之後，您將了解：</span><span class="sxs-lookup"><span data-stu-id="5bac1-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="5bac1-107">何謂 StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="5bac1-108">如何找出 StorSimple 裝置所處的模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="5bac1-109">如何從一般模式變更為維護模式 (反之亦然) </span><span class="sxs-lookup"><span data-stu-id="5bac1-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="5bac1-110">只能透過 StorSimple 裝置的 Windows PowerShell 介面執行上述的管理工作。</span><span class="sxs-lookup"><span data-stu-id="5bac1-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="5bac1-111">關於 StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-111">About StorSimple device modes</span></span>
<span data-ttu-id="5bac1-112">StorSimple 裝置可以在標準、維護和復原模式下運作。</span><span class="sxs-lookup"><span data-stu-id="5bac1-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="5bac1-113">以下簡短描述每一種模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="5bac1-114">標準模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-114">Normal mode</span></span>
<span data-ttu-id="5bac1-115">這定義為完整設定的 StorSimple 裝置的標準運作模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="5bac1-116">根據預設，您的裝置會以標準模式運作。</span><span class="sxs-lookup"><span data-stu-id="5bac1-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="5bac1-117">維護模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-117">Maintenance mode</span></span>
<span data-ttu-id="5bac1-118">有時候 StorSimple 裝置可能需要進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="5bac1-119">此模式可讓您在裝置上執行維護和安裝干擾性的更新，例如磁碟韌體的相關更新。</span><span class="sxs-lookup"><span data-stu-id="5bac1-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="5bac1-120">您只能透過 Windows PowerShell for StorSimple 讓系統進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="5bac1-121">在此模式中，所有的 I/O 要求都會暫停。</span><span class="sxs-lookup"><span data-stu-id="5bac1-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="5bac1-122">靜態隨機存取記憶體 (NVRAM) 之類的服務或叢集服務也會停止。</span><span class="sxs-lookup"><span data-stu-id="5bac1-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="5bac1-123">當您進入或結束此模式時，兩個控制器都會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5bac1-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="5bac1-124">當您結束維護模式時，所有的服務都將繼續執行，而且應該是健康情況良好。</span><span class="sxs-lookup"><span data-stu-id="5bac1-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="5bac1-125">這可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5bac1-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="5bac1-126">**僅正常運作的裝置才支援維護模式。其中有一或兩者未正常運作控制器的裝置不支援此模式。**
> </span><span class="sxs-lookup"><span data-stu-id="5bac1-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="5bac1-127">復原模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-127">Recovery mode</span></span>
<span data-ttu-id="5bac1-128">復原模式可以形容成「含網路支援的 Windows 安全模式」。</span><span class="sxs-lookup"><span data-stu-id="5bac1-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="5bac1-129">復原模式會連絡 Microsoft 支援服務小組，並允許他們在系統上執行診斷。</span><span class="sxs-lookup"><span data-stu-id="5bac1-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="5bac1-130">復原模式的主要目的是擷取系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5bac1-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="5bac1-131">如果您的系統進入復原模式，您應該連絡 Microsoft 支援服務來請示後續步驟。</span><span class="sxs-lookup"><span data-stu-id="5bac1-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="5bac1-132">如需詳細資訊，請移至 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="5bac1-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5bac1-133">**您無法將裝置設為復原模式。如果裝置處於錯誤狀態，復原模式會嘗試讓裝置進入可讓 Microsoft 支援服務人員檢查的狀態。**</span><span class="sxs-lookup"><span data-stu-id="5bac1-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="5bac1-134">判斷 StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="5bac1-135">判斷目前的裝置模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-135">To determine the current device mode</span></span>
1. <span data-ttu-id="5bac1-136">遵循 [使用 PuTTY 來連接到裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的步驟，登入裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="5bac1-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="5bac1-137">查看裝置的序列主控台功能表中的橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="5bac1-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="5bac1-138">此訊息會明確指出裝置處於維護模式或復原模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="5bac1-139">如果訊息不含任何關於系統模式的特定資訊，就表示裝置處於標準模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="5bac1-140">變更 StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="5bac1-141">您可以讓 StorSimple 裝置進入維護模式 (從標準模式)，以執行維護或安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="5bac1-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="5bac1-142">執行下列程序進入或結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bac1-143">進入維護模式之前，請存取 Azure 傳統入口網站中**維護**頁面上的**硬體狀態**，以確認兩個裝置控制器的健康情況良好。</span><span class="sxs-lookup"><span data-stu-id="5bac1-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="5bac1-144">如果一個或兩個控制器的健康情況不好，請連絡 Microsoft 支援服務以進行後續步驟。</span><span class="sxs-lookup"><span data-stu-id="5bac1-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="5bac1-145">如需詳細資訊，請移至 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="5bac1-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="5bac1-146">進入維護模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="5bac1-147">遵循 [使用 PuTTY 來連接到裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)中的步驟，登入裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="5bac1-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="5bac1-148">在序列主控台功能表中，選擇選項 1 [使用完整存取權登入] 。</span><span class="sxs-lookup"><span data-stu-id="5bac1-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5bac1-149">出現提示時，提供**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="5bac1-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="5bac1-150">預設密碼為：`Password1`。</span><span class="sxs-lookup"><span data-stu-id="5bac1-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="5bac1-151">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="5bac1-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="5bac1-152">您將會看到警告訊息，告知您維護模式將中斷所有 I/O 要求並提供與 Azure 傳統入口網站的連線，而系統將提示您進行確認。</span><span class="sxs-lookup"><span data-stu-id="5bac1-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="5bac1-153">輸入 **Y** 以進入維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="5bac1-154">這兩個控制站都將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5bac1-154">Both controllers will restart.</span></span> <span data-ttu-id="5bac1-155">完成重新啟動時，會出現另一個訊息，指出裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="5bac1-156">結束維護模式</span><span class="sxs-lookup"><span data-stu-id="5bac1-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="5bac1-157">登入裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="5bac1-157">Log on to the device serial console.</span></span> <span data-ttu-id="5bac1-158">從橫幅訊息確認您的裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="5bac1-159">在命令提示字元中，輸入：</span><span class="sxs-lookup"><span data-stu-id="5bac1-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="5bac1-160">隨即會出現警告訊息和確認訊息。</span><span class="sxs-lookup"><span data-stu-id="5bac1-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="5bac1-161">輸入 **Y** 以結束維護模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="5bac1-162">這兩個控制站都將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5bac1-162">Both controllers will restart.</span></span> <span data-ttu-id="5bac1-163">重新啟動完成時，會出現另一個訊息，指出裝置處於標準模式。</span><span class="sxs-lookup"><span data-stu-id="5bac1-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bac1-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bac1-164">Next steps</span></span>
<span data-ttu-id="5bac1-165">了解如何在 StorSimple 裝置上 [套用標準和維護模式更新](storsimple-update-device.md) 。</span><span class="sxs-lookup"><span data-stu-id="5bac1-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>
