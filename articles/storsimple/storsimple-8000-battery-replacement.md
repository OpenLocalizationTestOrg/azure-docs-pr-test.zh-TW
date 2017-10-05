---
title: "更換 Microsoft Azure StorSimple 8000 系列裝置上的電池 | Microsoft Docs"
description: "描述如何取下、更換和維護 StorSimple 裝置上的備份電池模組。"
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
ms.openlocfilehash: 174a3163082594ea6a49b7f5a78857848f8f0566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="44ab4-103">更換 StorSimple 裝置上的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-103">Replace the backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="44ab4-104">Overview</span><span class="sxs-lookup"><span data-stu-id="44ab4-104">Overview</span></span>
<span data-ttu-id="44ab4-105">Microsoft Azure StorSimple 裝置上的主要機箱電源和冷卻模組 (PCM) 具有額外的電池組。</span><span class="sxs-lookup"><span data-stu-id="44ab4-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="44ab4-106">這個電池組會提供電源，以便如果主要機箱失去 AC 電源，StorSimple 裝置可以儲存資料。</span><span class="sxs-lookup"><span data-stu-id="44ab4-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="44ab4-107">這個電池組稱為 *備份電池模組*。</span><span class="sxs-lookup"><span data-stu-id="44ab4-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="44ab4-108">備份電池模組僅針對 StorSimple 裝置中的主要機箱而存在 (EBOD 機箱未包含備份電池模組) 。</span><span class="sxs-lookup"><span data-stu-id="44ab4-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="44ab4-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="44ab4-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="44ab4-110">取下備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-110">Remove the backup battery module</span></span>
* <span data-ttu-id="44ab4-111">安裝新的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-111">Install a new backup battery module</span></span>
* <span data-ttu-id="44ab4-112">維護備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44ab4-113">取下及更換備份電池模組之前，請閱讀 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)中的安全資訊。</span><span class="sxs-lookup"><span data-stu-id="44ab4-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="44ab4-114">取下備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-114">Remove the backup battery module</span></span>
<span data-ttu-id="44ab4-115">StorSimple 裝置的備份電池模組是現場可置換裝置。</span><span class="sxs-lookup"><span data-stu-id="44ab4-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="44ab4-116">在 PCM 中安裝它之前，電池模組應該儲存在其原始包裝中。</span><span class="sxs-lookup"><span data-stu-id="44ab4-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="44ab4-117">執行下列步驟以取下備份電池。</span><span class="sxs-lookup"><span data-stu-id="44ab4-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="44ab4-118">若要取下備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="44ab4-119">在 Azure 入口網站中，移至您的 StorSimple 裝置管理員服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="44ab4-119">In the Azure portal, go to your StorSimple Device Manager service blade.</span></span> <span data-ttu-id="44ab4-120">移至 [裝置]，然後從裝置清單選取您的裝置。</span><span class="sxs-lookup"><span data-stu-id="44ab4-120">Go to **Devices** and then select your device from the list of devices.</span></span> <span data-ttu-id="44ab4-121">瀏覽至 [監視器] > [硬體健康情況]。</span><span class="sxs-lookup"><span data-stu-id="44ab4-121">Navigate to **Monitor** > **Hardware health**.</span></span> <span data-ttu-id="44ab4-122">在 [共用元件] 下，查看電池狀態。</span><span class="sxs-lookup"><span data-stu-id="44ab4-122">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="44ab4-123">識別電池故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="44ab4-123">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="44ab4-124">圖 1 顯示 StorSimple 裝置的背面。</span><span class="sxs-lookup"><span data-stu-id="44ab4-124">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![裝置主要機箱模組的後擋板](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="44ab4-126">**圖 1** 顯示 PCM 和控制器模組的主要裝置背面</span><span class="sxs-lookup"><span data-stu-id="44ab4-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="44ab4-127">標籤</span><span class="sxs-lookup"><span data-stu-id="44ab4-127">Label</span></span> | <span data-ttu-id="44ab4-128">說明</span><span class="sxs-lookup"><span data-stu-id="44ab4-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="44ab4-129">1</span><span class="sxs-lookup"><span data-stu-id="44ab4-129">1</span></span> |<span data-ttu-id="44ab4-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="44ab4-130">PCM 0</span></span> |
   | <span data-ttu-id="44ab4-131">2</span><span class="sxs-lookup"><span data-stu-id="44ab4-131">2</span></span> |<span data-ttu-id="44ab4-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="44ab4-132">PCM 1</span></span> |
   | <span data-ttu-id="44ab4-133">3</span><span class="sxs-lookup"><span data-stu-id="44ab4-133">3</span></span> |<span data-ttu-id="44ab4-134">控制器 0</span><span class="sxs-lookup"><span data-stu-id="44ab4-134">Controller 0</span></span> |
   | <span data-ttu-id="44ab4-135">4</span><span class="sxs-lookup"><span data-stu-id="44ab4-135">4</span></span> |<span data-ttu-id="44ab4-136">控制器 1</span><span class="sxs-lookup"><span data-stu-id="44ab4-136">Controller 1</span></span> |
   
    <span data-ttu-id="44ab4-137">如圖 2 中的號碼 3 所示，PCM 0 上對應到 **電池故障** 的監視指示器 LED 應該亮起。</span><span class="sxs-lookup"><span data-stu-id="44ab4-137">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="44ab4-139">**圖 2** 顯示監視指示器 LED 的 PCM 背面</span><span class="sxs-lookup"><span data-stu-id="44ab4-139">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="44ab4-140">標籤</span><span class="sxs-lookup"><span data-stu-id="44ab4-140">Label</span></span> | <span data-ttu-id="44ab4-141">說明</span><span class="sxs-lookup"><span data-stu-id="44ab4-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="44ab4-142">1</span><span class="sxs-lookup"><span data-stu-id="44ab4-142">1</span></span> |<span data-ttu-id="44ab4-143">AC 電源故障</span><span class="sxs-lookup"><span data-stu-id="44ab4-143">AC power failure</span></span> |
   | <span data-ttu-id="44ab4-144">2</span><span class="sxs-lookup"><span data-stu-id="44ab4-144">2</span></span> |<span data-ttu-id="44ab4-145">風扇故障</span><span class="sxs-lookup"><span data-stu-id="44ab4-145">Fan failure</span></span> |
   | <span data-ttu-id="44ab4-146">3</span><span class="sxs-lookup"><span data-stu-id="44ab4-146">3</span></span> |<span data-ttu-id="44ab4-147">電池故障</span><span class="sxs-lookup"><span data-stu-id="44ab4-147">Battery fault</span></span> |
   | <span data-ttu-id="44ab4-148">4</span><span class="sxs-lookup"><span data-stu-id="44ab4-148">4</span></span> |<span data-ttu-id="44ab4-149">PCM 正常</span><span class="sxs-lookup"><span data-stu-id="44ab4-149">PCM OK</span></span> |
   | <span data-ttu-id="44ab4-150">5</span><span class="sxs-lookup"><span data-stu-id="44ab4-150">5</span></span> |<span data-ttu-id="44ab4-151">DC 電源故障</span><span class="sxs-lookup"><span data-stu-id="44ab4-151">DC power failure</span></span> |
   | <span data-ttu-id="44ab4-152">6</span><span class="sxs-lookup"><span data-stu-id="44ab4-152">6</span></span> |<span data-ttu-id="44ab4-153">電池狀況良好</span><span class="sxs-lookup"><span data-stu-id="44ab4-153">Battery healthy</span></span> |
3. <span data-ttu-id="44ab4-154">若要取下電池故障的 PCM，請遵循 [取下 PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="44ab4-154">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="44ab4-155">一旦取下 PCM，請提起並向上旋轉電池模組把手 (如下圖中所示)，並將它拔出以取下電池。</span><span class="sxs-lookup"><span data-stu-id="44ab4-155">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![從 pcm 取出電池](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="44ab4-157">**圖 3** 從 PCM 取下電池</span><span class="sxs-lookup"><span data-stu-id="44ab4-157">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="44ab4-158">將模組放置在現場可更換裝置包裝中。</span><span class="sxs-lookup"><span data-stu-id="44ab4-158">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="44ab4-159">將故障裝置退回給 Microsoft，以取得適當的服務和處理。</span><span class="sxs-lookup"><span data-stu-id="44ab4-159">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="44ab4-160">安裝新的備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-160">Install a new backup battery module</span></span>
<span data-ttu-id="44ab4-161">執行下列步驟，以在 StorSimple 裝置的主要機箱中的 PCM 安裝更換電池模組。</span><span class="sxs-lookup"><span data-stu-id="44ab4-161">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="44ab4-162">若要安裝電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-162">To install the battery module</span></span>
1. <span data-ttu-id="44ab4-163">以適當的方向將備份電池模組放入 PCM 中。</span><span class="sxs-lookup"><span data-stu-id="44ab4-163">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="44ab4-164">全力按壓電池模組把手以固定連接器。</span><span class="sxs-lookup"><span data-stu-id="44ab4-164">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="44ab4-165">依照 [更換 StorSimple 裝置上的電源和冷卻模組](storsimple-power-cooling-module-replacement.md)中的指導方針，更換主要機箱的 PCM。</span><span class="sxs-lookup"><span data-stu-id="44ab4-165">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="44ab4-166">在更換完成之後，請移至您的裝置，然後在 Azure 入口網站移至 [監視器] > [硬體健康情況]。</span><span class="sxs-lookup"><span data-stu-id="44ab4-166">After the replacement is complete, go to your device and then go to **Monitor** > **Hardware health** in the Azure portal.</span></span> <span data-ttu-id="44ab4-167">確認電池的狀態，以確定安裝成功。</span><span class="sxs-lookup"><span data-stu-id="44ab4-167">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="44ab4-168">綠色狀態表示電池狀況良好。</span><span class="sxs-lookup"><span data-stu-id="44ab4-168">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="44ab4-169">維護備份電池模組</span><span class="sxs-lookup"><span data-stu-id="44ab4-169">Maintain the backup battery module</span></span>
<span data-ttu-id="44ab4-170">在 StorSimple 裝置中，備份電池模組會在停電期間提供電源給控制器。</span><span class="sxs-lookup"><span data-stu-id="44ab4-170">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="44ab4-171">它可讓 StorSimple 裝置在以控制方式關閉之前儲存重要資料。</span><span class="sxs-lookup"><span data-stu-id="44ab4-171">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="44ab4-172">由於 PCM 中有兩個完全充電的電池，系統可以處理兩個連續停電事件。</span><span class="sxs-lookup"><span data-stu-id="44ab4-172">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="44ab4-173">在 Azure 入口網站中，[監視器] 刀鋒視窗下的 [硬體健康情況] 指出電池是否故障，或電力何時即將用光。</span><span class="sxs-lookup"><span data-stu-id="44ab4-173">In the Azure portal, the **Hardware health** under the **Monitor** blade indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="44ab4-174">在 [共用元件] 下，電池狀態是以 [PCM 1 中的電池] 或 [PCM 0 中的電池] 指出。</span><span class="sxs-lookup"><span data-stu-id="44ab4-174">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="44ab4-175">此刀鋒視窗會顯示 [降級] 狀態，表示電力即將用光，或顯示 [故障]，表示電力已用光。</span><span class="sxs-lookup"><span data-stu-id="44ab4-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="44ab4-176">當電池只需充電時，可以報告 [ **故障** ]。</span><span class="sxs-lookup"><span data-stu-id="44ab4-176">The battery can report **FAILED** when it simply needs to be charged.</span></span>


<span data-ttu-id="44ab4-177">如果 [ **降級** ] 狀態出現，我們建議採取下列動作：</span><span class="sxs-lookup"><span data-stu-id="44ab4-177">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="44ab4-178">系統最近可能遭遇停電，或電池可能正在進行定期維護。</span><span class="sxs-lookup"><span data-stu-id="44ab4-178">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="44ab4-179">觀察系統 12 小時，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="44ab4-179">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="44ab4-180">在連續 12 小時連接至 AC 電源，而且控制器與 PCM 正在執行之後，如果狀態仍為 [ **降級** ]，則需要更換電池。</span><span class="sxs-lookup"><span data-stu-id="44ab4-180">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="44ab4-181">請 [連絡 Microsoft 支援](storsimple-8000-contact-microsoft-support.md) ，以取得更換備份電池模組。</span><span class="sxs-lookup"><span data-stu-id="44ab4-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="44ab4-182">如果狀態在 12 小時之後變成良好，則電池可操作，而且只需維護費用。</span><span class="sxs-lookup"><span data-stu-id="44ab4-182">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="44ab4-183">如果沒有相關聯的 AC 電源喪失，而且 PCM 已開啟並連接至 AC 電源，則電池需要更換。</span><span class="sxs-lookup"><span data-stu-id="44ab4-183">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="44ab4-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) ，以訂購更換備份電池模組。</span><span class="sxs-lookup"><span data-stu-id="44ab4-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44ab4-185">依據國家及地區法規處置故障電池。</span><span class="sxs-lookup"><span data-stu-id="44ab4-185">Dispose of the failed battery according to national and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44ab4-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44ab4-186">Next steps</span></span>
<span data-ttu-id="44ab4-187">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="44ab4-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

