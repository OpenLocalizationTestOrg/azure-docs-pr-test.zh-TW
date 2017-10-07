---
title: "Microsoft Azure StorSimple 裝置上的 aaaReplace 電池 |Microsoft 文件"
description: "描述如何 tooremove，取代，並維護您的 StorSimple 裝置上的 hello 備用電池模組。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="497fa-103">取代您的 StorSimple 裝置上的 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="497fa-104">概觀</span><span class="sxs-lookup"><span data-stu-id="497fa-104">Overview</span></span>
<span data-ttu-id="497fa-105">hello 主要機箱電源和冷卻模組 (PCM) 在您的 Microsoft Azure StorSimple 裝置上都有額外的電池組。</span><span class="sxs-lookup"><span data-stu-id="497fa-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="497fa-106">此組件提供電源，以便 hello StorSimple 裝置可以將資料儲存是否有遺失的 AC 電源 toohello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="497fa-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="497fa-107">這個電池組會參照的 tooas hello*備用電池模組*。</span><span class="sxs-lookup"><span data-stu-id="497fa-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="497fa-108">hello 備用電池模組僅存在您的 StorSimple 裝置中的 hello 主要機箱 （hello EBOD 機箱不包含備用電池模組）。</span><span class="sxs-lookup"><span data-stu-id="497fa-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="497fa-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="497fa-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="497fa-110">移除 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="497fa-111">安裝新的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-111">Install a new backup battery module</span></span>
* <span data-ttu-id="497fa-112">維護 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="497fa-113">移除和更換備用電池模組時，檢閱 hello hello 安全性資訊之前[簡介 tooStorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="497fa-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="497fa-114">移除 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-114">Remove hello backup battery module</span></span>
<span data-ttu-id="497fa-115">您的 StorSimple 裝置 hello 備用電池模組是欄位置換單元。</span><span class="sxs-lookup"><span data-stu-id="497fa-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="497fa-116">它會安裝在 hello PCM 之前，hello 電池模組應存放在其原始包裝。</span><span class="sxs-lookup"><span data-stu-id="497fa-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="497fa-117">執行下列步驟 tooremove hello 備用電池的 hello。</span><span class="sxs-lookup"><span data-stu-id="497fa-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="497fa-118">tooremove hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="497fa-119">在 hello Azure 傳統入口網站中移過**裝置** > **維護** > **硬體狀態**。</span><span class="sxs-lookup"><span data-stu-id="497fa-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="497fa-120">在下**共用元件**，查看 hello hello 電池狀態。</span><span class="sxs-lookup"><span data-stu-id="497fa-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="497fa-121">識別 hello 中的 hello 電池故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="497fa-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="497fa-122">圖 1 顯示 hello hello StorSimple 裝置背面。</span><span class="sxs-lookup"><span data-stu-id="497fa-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="497fa-124">**圖 1** 顯示 PCM 和控制器模組的主要裝置背面</span><span class="sxs-lookup"><span data-stu-id="497fa-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="497fa-125">標籤</span><span class="sxs-lookup"><span data-stu-id="497fa-125">Label</span></span> | <span data-ttu-id="497fa-126">說明</span><span class="sxs-lookup"><span data-stu-id="497fa-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="497fa-127">1</span><span class="sxs-lookup"><span data-stu-id="497fa-127">1</span></span> |<span data-ttu-id="497fa-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="497fa-128">PCM 0</span></span> |
   | <span data-ttu-id="497fa-129">2</span><span class="sxs-lookup"><span data-stu-id="497fa-129">2</span></span> |<span data-ttu-id="497fa-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="497fa-130">PCM 1</span></span> |
   | <span data-ttu-id="497fa-131">3</span><span class="sxs-lookup"><span data-stu-id="497fa-131">3</span></span> |<span data-ttu-id="497fa-132">控制器 0</span><span class="sxs-lookup"><span data-stu-id="497fa-132">Controller 0</span></span> |
   | <span data-ttu-id="497fa-133">4</span><span class="sxs-lookup"><span data-stu-id="497fa-133">4</span></span> |<span data-ttu-id="497fa-134">控制器 1</span><span class="sxs-lookup"><span data-stu-id="497fa-134">Controller 1</span></span> |
   
    <span data-ttu-id="497fa-135">Hello 圖 2 中的編號 3 所示，hello 監控指示器 LED 太對應的 PCM 0 上**電池故障**應亮起。</span><span class="sxs-lookup"><span data-stu-id="497fa-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="497fa-137">**圖 2**監控指示器 Led 的 PCM 背面顯示 hello</span><span class="sxs-lookup"><span data-stu-id="497fa-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="497fa-138">標籤</span><span class="sxs-lookup"><span data-stu-id="497fa-138">Label</span></span> | <span data-ttu-id="497fa-139">說明</span><span class="sxs-lookup"><span data-stu-id="497fa-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="497fa-140">1</span><span class="sxs-lookup"><span data-stu-id="497fa-140">1</span></span> |<span data-ttu-id="497fa-141">AC 電源故障</span><span class="sxs-lookup"><span data-stu-id="497fa-141">AC power failure</span></span> |
   | <span data-ttu-id="497fa-142">2</span><span class="sxs-lookup"><span data-stu-id="497fa-142">2</span></span> |<span data-ttu-id="497fa-143">風扇故障</span><span class="sxs-lookup"><span data-stu-id="497fa-143">Fan failure</span></span> |
   | <span data-ttu-id="497fa-144">3</span><span class="sxs-lookup"><span data-stu-id="497fa-144">3</span></span> |<span data-ttu-id="497fa-145">電池故障</span><span class="sxs-lookup"><span data-stu-id="497fa-145">Battery fault</span></span> |
   | <span data-ttu-id="497fa-146">4</span><span class="sxs-lookup"><span data-stu-id="497fa-146">4</span></span> |<span data-ttu-id="497fa-147">PCM 正常</span><span class="sxs-lookup"><span data-stu-id="497fa-147">PCM OK</span></span> |
   | <span data-ttu-id="497fa-148">5</span><span class="sxs-lookup"><span data-stu-id="497fa-148">5</span></span> |<span data-ttu-id="497fa-149">DC 電源故障</span><span class="sxs-lookup"><span data-stu-id="497fa-149">DC power failure</span></span> |
   | <span data-ttu-id="497fa-150">6</span><span class="sxs-lookup"><span data-stu-id="497fa-150">6</span></span> |<span data-ttu-id="497fa-151">電池狀況良好</span><span class="sxs-lookup"><span data-stu-id="497fa-151">Battery healthy</span></span> |
3. <span data-ttu-id="497fa-152">tooremove hello PCM 電池故障，請依照下列中的 hello 步驟[移除 PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm)。</span><span class="sxs-lookup"><span data-stu-id="497fa-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="497fa-153">已卸下 PCM hello、 增益與 hello 旋轉電池模組向上處理 hello 下列圖表所示，提取 tooremove hello 電池。</span><span class="sxs-lookup"><span data-stu-id="497fa-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![從 pcm 取出電池](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="497fa-155">**圖 3**正在從 hello PCM hello 電池</span><span class="sxs-lookup"><span data-stu-id="497fa-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="497fa-156">Hello 模組置於 hello 欄位置換單元封裝。</span><span class="sxs-lookup"><span data-stu-id="497fa-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="497fa-157">傳回適當的服務和處理 hello 故障單元 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="497fa-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="497fa-158">安裝新的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-158">Install a new backup battery module</span></span>
<span data-ttu-id="497fa-159">執行下列步驟 tooinstall hello 更換電池模組在您的 StorSimple 裝置 hello 主要機箱中的 hello PCM 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="497fa-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="497fa-160">tooinstall hello 電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="497fa-161">將 hello 備用電池模組放在 hello PCM 中的 hello 適當方向。</span><span class="sxs-lookup"><span data-stu-id="497fa-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="497fa-162">按向下 hello 電池模組會處理所有的 hello 方式 tooseat hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="497fa-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="497fa-163">取代 hello hello 主要機箱中的 PCM，依照下列中的 hello 指導方針[取代您的 StorSimple 裝置上的電源和冷卻模組](storsimple-power-cooling-module-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="497fa-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="497fa-164">Hello 更換完成之後，請跳過**裝置** > **維護** > **硬體狀態**hello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="497fa-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="497fa-165">確認 hello hello 電池 toomake 確定 hello 安裝成功狀態。</span><span class="sxs-lookup"><span data-stu-id="497fa-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="497fa-166">綠色狀態表示 hello 電池狀況良好。</span><span class="sxs-lookup"><span data-stu-id="497fa-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="497fa-167">維護 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="497fa-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="497fa-168">在您的 StorSimple 裝置 hello 備用電池模組會提供電源 toohello 控制器發生斷電事件期間。</span><span class="sxs-lookup"><span data-stu-id="497fa-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="497fa-169">它允許 hello StorSimple 裝置 toosave 重要資料先前 tooshutting 下的以節制的方式。</span><span class="sxs-lookup"><span data-stu-id="497fa-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="497fa-170">與 hello Pcm 中兩個完全充電的電池，hello 系統可以處理兩個連續斷電事件。</span><span class="sxs-lookup"><span data-stu-id="497fa-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="497fa-171">Hello Azure 傳統入口網站，在 hello**硬體狀態**上 hello**維護**頁面會指出是否 hello 電池無法正常運作或已接近 hello 生命結束。</span><span class="sxs-lookup"><span data-stu-id="497fa-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="497fa-172">hello 電池狀態由**PCM 0 中的電池**或**PCM 1 中的電池**下**共用元件**。</span><span class="sxs-lookup"><span data-stu-id="497fa-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="497fa-173">此頁面會顯示 [降級] 狀態，表示電池即將用光，以及顯示 [故障]，表示電池已用光。</span><span class="sxs-lookup"><span data-stu-id="497fa-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="497fa-174">hello 電池可以報告**失敗**只需要支付 toobe 時。</span><span class="sxs-lookup"><span data-stu-id="497fa-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="497fa-175">如果 hello**降級**狀態出現，我們建議 hello 之後採取的動作：</span><span class="sxs-lookup"><span data-stu-id="497fa-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="497fa-176">hello 系統發生新的電源中斷或 hello 電池可能正在進行定期維護。</span><span class="sxs-lookup"><span data-stu-id="497fa-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="497fa-177">觀察 hello 系統 12 個小時後再繼續。</span><span class="sxs-lookup"><span data-stu-id="497fa-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="497fa-178">如果 hello 狀態仍**降級**12 小時的持續連接 tooAC 電源以 hello 控制器與 Pcm 執行，然後 hello 之後需要 toobe 更換電池。</span><span class="sxs-lookup"><span data-stu-id="497fa-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="497fa-179">請 [連絡 Microsoft 支援](storsimple-contact-microsoft-support.md) ，以取得更換備份電池模組。</span><span class="sxs-lookup"><span data-stu-id="497fa-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="497fa-180">如果 hello 後狀態變成 OK 12 小時，hello 電池運作，以及它只需維護費用。</span><span class="sxs-lookup"><span data-stu-id="497fa-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="497fa-181">如果沒有相關聯的失去 AC 電源和 hello PCM 已開啟且連線 tooAC 電源，需要取代 toobe hello 電池。</span><span class="sxs-lookup"><span data-stu-id="497fa-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="497fa-182">[請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)tooorder 更換備份電池模組。</span><span class="sxs-lookup"><span data-stu-id="497fa-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="497fa-183">處置 hello 無法根據 toonational 及地區法規的電池。</span><span class="sxs-lookup"><span data-stu-id="497fa-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="497fa-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="497fa-184">Next steps</span></span>
<span data-ttu-id="497fa-185">深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="497fa-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

