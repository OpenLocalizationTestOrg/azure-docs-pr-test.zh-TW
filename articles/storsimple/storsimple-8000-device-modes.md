---
title: "aaaChange StorSimple 裝置模式 |Microsoft 文件"
description: "描述 hello StorSimple 裝置模式，並說明如何 toouse Windows PowerShell for StorSimple toochange hello 裝置模式。"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="5e9b9-103">變更您的 StorSimple 裝置上的 hello 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="5e9b9-104">本文章會提供各種不同的模式，您的 StorSimple 裝置能 hello 的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="5e9b9-105">StorSimple 裝置有三種運作模式：標準、維護和復原。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="5e9b9-106">閱讀本文之後，您將了解：</span><span class="sxs-lookup"><span data-stu-id="5e9b9-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="5e9b9-107">Hello StorSimple 裝置模式為何</span><span class="sxs-lookup"><span data-stu-id="5e9b9-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="5e9b9-108">Toofigure 出哪些模式 hello StorSimple 裝置的方式是在</span><span class="sxs-lookup"><span data-stu-id="5e9b9-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="5e9b9-109">如何從一般 toomaintenance 模式 toochange 和*反之亦然*</span><span class="sxs-lookup"><span data-stu-id="5e9b9-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="5e9b9-110">hello 上方管理工作只能透過您的 StorSimple 裝置 hello Windows PowerShell 介面執行。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="5e9b9-111">關於 StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-111">About StorSimple device modes</span></span>

<span data-ttu-id="5e9b9-112">StorSimple 裝置可以在標準、維護和復原模式下運作。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="5e9b9-113">以下簡短描述每一種模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="5e9b9-114">標準模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-114">Normal mode</span></span>

<span data-ttu-id="5e9b9-115">這被定義為 hello 正常作業模式的完整設定 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="5e9b9-116">根據預設，您的裝置會以標準模式運作。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="5e9b9-117">維護模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-117">Maintenance mode</span></span>

<span data-ttu-id="5e9b9-118">有時候 hello StorSimple 裝置可能需要 toobe 放入維護模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="5e9b9-119">這個模式可讓您在 hello 裝置上的 tooperform 維護，而且安裝更新具有干擾性，例如那些相關 toodisk 韌體。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="5e9b9-120">您可以進入 hello 系統維護模式僅透過 hello Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="5e9b9-121">在此模式中，所有的 I/O 要求都會暫停。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="5e9b9-122">也會停止服務，例如非揮發性隨機存取記憶體 (NVRAM) 或 hello 叢集服務。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="5e9b9-123">當您進入或退出此模式中，兩個 hello 控制器會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="5e9b9-124">當您結束 hello 維護模式時，所有的 hello 服務將會繼續，而且應該是狀況良好。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="5e9b9-125">這可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="5e9b9-126">**僅正常運作的裝置才支援維護模式。不支援在其中之一或兩者的 hello 控制器無法運作的裝置上。**</span><span class="sxs-lookup"><span data-stu-id="5e9b9-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="5e9b9-127">復原模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-127">Recovery mode</span></span>

<span data-ttu-id="5e9b9-128">復原模式可以形容成「含網路支援的 Windows 安全模式」。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="5e9b9-129">復原模式會 hello Microsoft 支援服務團隊，並讓他們 tooperform 診斷 hello 系統上。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="5e9b9-130">hello 的復原模式的主要目標是 tooretrieve hello 系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="5e9b9-131">如果您的系統進入復原模式，您應該連絡 Microsoft 支援服務來請示後續步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="5e9b9-132">如需詳細資訊，請移至太[請連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5e9b9-133">**您不能放置 hello 裝置進入修復模式。如果 hello 裝置處於不正常的狀態，復原模式會嘗試 tooget hello 裝置進入 Microsoft 支援人員可以檢查它的狀態。**</span><span class="sxs-lookup"><span data-stu-id="5e9b9-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="5e9b9-134">判斷 StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="5e9b9-135">toodetermine hello 目前裝置模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="5e9b9-136">登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="5e9b9-137">查看 hello hello 裝置序列主控台功能表中的 hello 橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="5e9b9-138">此訊息會明確指出 hello 裝置是否為維護或復原模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="5e9b9-139">如果 hello 訊息沒有任何相關 toohello 系統模式的特定資訊，請 hello 裝置處於正常模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="5e9b9-140">變更 hello StorSimple 裝置模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="5e9b9-141">您可以將 hello StorSimple 裝置放入維護模式 （從標準模式） tooperform 維護或安裝維護模式更新。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="5e9b9-142">執行下列程序 tooenter 或離開維護模式的 hello。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e9b9-143">之前進入維護模式，請確認兩個裝置控制器會處於狀況良好，藉由存取 hello**裝置設定 > 硬體健全狀況**為您的裝置 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="5e9b9-144">如果一或兩個 hello 控制站狀況良好，請連絡 Microsoft 支援 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="5e9b9-145">如需詳細資訊，請移至太[請連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="5e9b9-146">tooenter 維護模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="5e9b9-147">登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="5e9b9-148">在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5e9b9-149">出現提示時，提供 hello**裝置系統管理員密碼**。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="5e9b9-150">hello 預設密碼為： `Password1`。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="5e9b9-151">在 hello 命令提示字元中輸入</span><span class="sxs-lookup"><span data-stu-id="5e9b9-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="5e9b9-152">您會看到警告訊息，告知您該維護模式將會中斷所有的 I/O 要求並切斷 hello 連接 toohello Azure 入口網站，系統將提示您確認。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="5e9b9-153">型別**Y** tooenter 維護模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="5e9b9-154">這兩個控制站都將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-154">Both controllers will restart.</span></span> <span data-ttu-id="5e9b9-155">Hello 重新啟動完成時，會指出 hello 序列主控台橫幅，該 hello 裝置處於維護模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="5e9b9-156">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="5e9b9-157">tooexit 維護模式</span><span class="sxs-lookup"><span data-stu-id="5e9b9-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="5e9b9-158">登入 toohello 裝置序列主控台。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-158">Log on toohello device serial console.</span></span> <span data-ttu-id="5e9b9-159">請確認從您的裝置處於維護模式的 hello 橫幅訊息。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="5e9b9-160">在 hello 命令提示字元中輸入：</span><span class="sxs-lookup"><span data-stu-id="5e9b9-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="5e9b9-161">隨即會出現警告訊息和確認訊息。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="5e9b9-162">型別**Y** tooexit 維護模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="5e9b9-163">這兩個控制站都將重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-163">Both controllers will restart.</span></span> <span data-ttu-id="5e9b9-164">Hello 重新啟動完成時，hello 序列主控台橫幅指出該 hello 裝置處於正常模式。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="5e9b9-165">下方顯示一項範例輸出。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="5e9b9-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e9b9-166">Next steps</span></span>

<span data-ttu-id="5e9b9-167">了解如何太[適用於 [標準] 和 [維護模式更新](storsimple-update-device.md)StorSimple 裝置上。</span><span class="sxs-lookup"><span data-stu-id="5e9b9-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

