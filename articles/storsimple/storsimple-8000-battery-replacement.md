---
title: "Microsoft Azure StorSimple 8000 系列裝置 aaaReplace 電池電力 |Microsoft 文件"
description: "描述如何 tooremove，取代，並維護您的 StorSimple 裝置上的 hello 備用電池模組。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="1db30-103">取代您的 StorSimple 裝置上的 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="1db30-104">概觀</span><span class="sxs-lookup"><span data-stu-id="1db30-104">Overview</span></span>
<span data-ttu-id="1db30-105">hello 主要機箱電源和冷卻模組 (PCM) 在您的 Microsoft Azure StorSimple 裝置上都有額外的電池組。</span><span class="sxs-lookup"><span data-stu-id="1db30-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="1db30-106">此組件提供電源，以便 hello StorSimple 裝置可以將資料儲存是否有遺失的 AC 電源 toohello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="1db30-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="1db30-107">這個電池組會參照的 tooas hello*備用電池模組*。</span><span class="sxs-lookup"><span data-stu-id="1db30-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="1db30-108">hello 備用電池模組僅存在您的 StorSimple 裝置中的 hello 主要機箱 （hello EBOD 機箱不包含備用電池模組）。</span><span class="sxs-lookup"><span data-stu-id="1db30-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="1db30-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="1db30-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="1db30-110">移除 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="1db30-111">安裝新的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-111">Install a new backup battery module</span></span>
* <span data-ttu-id="1db30-112">維護 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1db30-113">移除和更換備用電池模組時，檢閱 hello hello 安全性資訊之前[簡介 tooStorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="1db30-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="1db30-114">移除 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-114">Remove hello backup battery module</span></span>
<span data-ttu-id="1db30-115">您的 StorSimple 裝置 hello 備用電池模組是欄位置換單元。</span><span class="sxs-lookup"><span data-stu-id="1db30-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="1db30-116">它會安裝在 hello PCM 之前，hello 電池模組應存放在其原始包裝。</span><span class="sxs-lookup"><span data-stu-id="1db30-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="1db30-117">執行下列步驟 tooremove hello 備用電池的 hello。</span><span class="sxs-lookup"><span data-stu-id="1db30-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="1db30-118">tooremove hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="1db30-119">在 hello Azure 入口網站，移 tooyour StorSimple 裝置管理員服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1db30-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="1db30-120">跳過**裝置**，然後從 hello 的裝置清單中選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="1db30-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="1db30-121">瀏覽過**監視器** > **硬體健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="1db30-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="1db30-122">在下**共用元件**，查看 hello hello 電池狀態。</span><span class="sxs-lookup"><span data-stu-id="1db30-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="1db30-123">識別 hello 中的 hello 電池故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="1db30-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="1db30-124">圖 1 顯示 hello hello StorSimple 裝置背面。</span><span class="sxs-lookup"><span data-stu-id="1db30-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="1db30-126">**圖 1** 顯示 PCM 和控制器模組的主要裝置背面</span><span class="sxs-lookup"><span data-stu-id="1db30-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="1db30-127">標籤</span><span class="sxs-lookup"><span data-stu-id="1db30-127">Label</span></span> | <span data-ttu-id="1db30-128">說明</span><span class="sxs-lookup"><span data-stu-id="1db30-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1db30-129">1</span><span class="sxs-lookup"><span data-stu-id="1db30-129">1</span></span> |<span data-ttu-id="1db30-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="1db30-130">PCM 0</span></span> |
   | <span data-ttu-id="1db30-131">2</span><span class="sxs-lookup"><span data-stu-id="1db30-131">2</span></span> |<span data-ttu-id="1db30-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="1db30-132">PCM 1</span></span> |
   | <span data-ttu-id="1db30-133">3</span><span class="sxs-lookup"><span data-stu-id="1db30-133">3</span></span> |<span data-ttu-id="1db30-134">控制器 0</span><span class="sxs-lookup"><span data-stu-id="1db30-134">Controller 0</span></span> |
   | <span data-ttu-id="1db30-135">4</span><span class="sxs-lookup"><span data-stu-id="1db30-135">4</span></span> |<span data-ttu-id="1db30-136">控制器 1</span><span class="sxs-lookup"><span data-stu-id="1db30-136">Controller 1</span></span> |
   
    <span data-ttu-id="1db30-137">Hello 圖 2 中的編號 3 所示，hello 監控指示器 LED 太對應的 PCM 0 上**電池故障**應亮起。</span><span class="sxs-lookup"><span data-stu-id="1db30-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="1db30-139">**圖 2**監控指示器 Led 的 PCM 背面顯示 hello</span><span class="sxs-lookup"><span data-stu-id="1db30-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="1db30-140">標籤</span><span class="sxs-lookup"><span data-stu-id="1db30-140">Label</span></span> | <span data-ttu-id="1db30-141">說明</span><span class="sxs-lookup"><span data-stu-id="1db30-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1db30-142">1</span><span class="sxs-lookup"><span data-stu-id="1db30-142">1</span></span> |<span data-ttu-id="1db30-143">AC 電源故障</span><span class="sxs-lookup"><span data-stu-id="1db30-143">AC power failure</span></span> |
   | <span data-ttu-id="1db30-144">2</span><span class="sxs-lookup"><span data-stu-id="1db30-144">2</span></span> |<span data-ttu-id="1db30-145">風扇故障</span><span class="sxs-lookup"><span data-stu-id="1db30-145">Fan failure</span></span> |
   | <span data-ttu-id="1db30-146">3</span><span class="sxs-lookup"><span data-stu-id="1db30-146">3</span></span> |<span data-ttu-id="1db30-147">電池故障</span><span class="sxs-lookup"><span data-stu-id="1db30-147">Battery fault</span></span> |
   | <span data-ttu-id="1db30-148">4</span><span class="sxs-lookup"><span data-stu-id="1db30-148">4</span></span> |<span data-ttu-id="1db30-149">PCM 正常</span><span class="sxs-lookup"><span data-stu-id="1db30-149">PCM OK</span></span> |
   | <span data-ttu-id="1db30-150">5</span><span class="sxs-lookup"><span data-stu-id="1db30-150">5</span></span> |<span data-ttu-id="1db30-151">DC 電源故障</span><span class="sxs-lookup"><span data-stu-id="1db30-151">DC power failure</span></span> |
   | <span data-ttu-id="1db30-152">6</span><span class="sxs-lookup"><span data-stu-id="1db30-152">6</span></span> |<span data-ttu-id="1db30-153">電池狀況良好</span><span class="sxs-lookup"><span data-stu-id="1db30-153">Battery healthy</span></span> |
3. <span data-ttu-id="1db30-154">tooremove hello PCM 電池故障，請依照下列中的 hello 步驟[移除 PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm)。</span><span class="sxs-lookup"><span data-stu-id="1db30-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="1db30-155">已卸下 PCM hello、 增益與 hello 旋轉電池模組向上處理 hello 下列圖表所示，提取 tooremove hello 電池。</span><span class="sxs-lookup"><span data-stu-id="1db30-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![從 pcm 取出電池](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="1db30-157">**圖 3**正在從 hello PCM hello 電池</span><span class="sxs-lookup"><span data-stu-id="1db30-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="1db30-158">Hello 模組置於 hello 欄位置換單元封裝。</span><span class="sxs-lookup"><span data-stu-id="1db30-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="1db30-159">傳回適當的服務和處理 hello 故障單元 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="1db30-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="1db30-160">安裝新的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-160">Install a new backup battery module</span></span>
<span data-ttu-id="1db30-161">執行下列步驟 tooinstall hello 更換電池模組在您的 StorSimple 裝置 hello 主要機箱中的 hello PCM 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1db30-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="1db30-162">tooinstall hello 電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="1db30-163">將 hello 備用電池模組放在 hello PCM 中的 hello 適當方向。</span><span class="sxs-lookup"><span data-stu-id="1db30-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="1db30-164">按向下 hello 電池模組會處理所有的 hello 方式 tooseat hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="1db30-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="1db30-165">取代 hello hello 主要機箱中的 PCM，依照下列中的 hello 指導方針[取代您的 StorSimple 裝置上的電源和冷卻模組](storsimple-power-cooling-module-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="1db30-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="1db30-166">Hello 更換完成之後，請移 tooyour 裝置，並前往太**監視器** > **硬體健全狀況**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="1db30-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="1db30-167">確認 hello hello 電池 toomake 確定 hello 安裝成功狀態。</span><span class="sxs-lookup"><span data-stu-id="1db30-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="1db30-168">綠色狀態表示 hello 電池狀況良好。</span><span class="sxs-lookup"><span data-stu-id="1db30-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="1db30-169">維護 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="1db30-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="1db30-170">在您的 StorSimple 裝置 hello 備用電池模組會提供電源 toohello 控制器發生斷電事件期間。</span><span class="sxs-lookup"><span data-stu-id="1db30-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="1db30-171">它允許 hello StorSimple 裝置 toosave 重要資料先前 tooshutting 下的以節制的方式。</span><span class="sxs-lookup"><span data-stu-id="1db30-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="1db30-172">與 hello Pcm 中兩個完全充電的電池，hello 系統可以處理兩個連續斷電事件。</span><span class="sxs-lookup"><span data-stu-id="1db30-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="1db30-173">Hello Azure 入口網站，在 hello**硬體健全狀況**下 hello**監視器**刀鋒視窗中會指出 hello 電池無法正常運作或已接近 hello 生命結束。</span><span class="sxs-lookup"><span data-stu-id="1db30-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="1db30-174">hello 電池狀態由**PCM 0 中的電池**或**PCM 1 中的電池**下**共用元件**。</span><span class="sxs-lookup"><span data-stu-id="1db30-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="1db30-175">此刀鋒視窗會顯示 [降級] 狀態，表示電力即將用光，或顯示 [故障]，表示電力已用光。</span><span class="sxs-lookup"><span data-stu-id="1db30-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="1db30-176">hello 電池可以報告**失敗**只需要支付 toobe 時。</span><span class="sxs-lookup"><span data-stu-id="1db30-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="1db30-177">如果 hello**降級**狀態出現，我們建議 hello 之後採取的動作：</span><span class="sxs-lookup"><span data-stu-id="1db30-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="1db30-178">hello 系統發生新的電源中斷或 hello 電池可能正在進行定期維護。</span><span class="sxs-lookup"><span data-stu-id="1db30-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="1db30-179">觀察 hello 系統 12 個小時後再繼續。</span><span class="sxs-lookup"><span data-stu-id="1db30-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="1db30-180">如果 hello 狀態仍**降級**12 小時的持續連接 tooAC 電源以 hello 控制器與 Pcm 執行，然後 hello 之後需要 toobe 更換電池。</span><span class="sxs-lookup"><span data-stu-id="1db30-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="1db30-181">請 [連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md) ，以取得更換備份電池模組。</span><span class="sxs-lookup"><span data-stu-id="1db30-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="1db30-182">如果 hello 後狀態變成 OK 12 小時，hello 電池運作，以及它只需維護費用。</span><span class="sxs-lookup"><span data-stu-id="1db30-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="1db30-183">如果沒有相關聯的失去 AC 電源和 hello PCM 已開啟且連線 tooAC 電源，需要取代 toobe hello 電池。</span><span class="sxs-lookup"><span data-stu-id="1db30-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="1db30-184">[請連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md)tooorder 更換備份電池模組。</span><span class="sxs-lookup"><span data-stu-id="1db30-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1db30-185">處置 hello 無法根據 toonational 及地區法規的電池。</span><span class="sxs-lookup"><span data-stu-id="1db30-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1db30-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1db30-186">Next steps</span></span>
<span data-ttu-id="1db30-187">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="1db30-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

