---
title: "更換 StorSimple 裝置上的 PCM | Microsoft Docs"
description: "說明如何取下及更換 StorSimple 裝置上的電源和冷卻模組"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 2a956de58b279a013913631a077d7b03c6327f72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="2b605-103">更換 StorSimple 裝置上的電源和冷卻模組</span><span class="sxs-lookup"><span data-stu-id="2b605-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="2b605-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2b605-104">Overview</span></span>
<span data-ttu-id="2b605-105">Microsoft Azure StorSimple 裝置的電源和冷卻模組 (PCM) 包含電源供應器和冷卻風扇，是透過主要及 EBOD 機箱控制。</span><span class="sxs-lookup"><span data-stu-id="2b605-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="2b605-106">每個機箱只有一個認證的 PCM 模型。</span><span class="sxs-lookup"><span data-stu-id="2b605-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="2b605-107">764 W PCM 是認證的主要機箱， 580 W PCM 是認證的 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="2b605-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="2b605-108">雖然主要機箱和 EBOD 機箱的 PCM 不同，更換程序完全相同。</span><span class="sxs-lookup"><span data-stu-id="2b605-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="2b605-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="2b605-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="2b605-110">取下 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-110">Remove a PCM</span></span>
* <span data-ttu-id="2b605-111">安裝替代的 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b605-112">取下及更換 PCM 之前，請閱讀 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)中的安全資訊。</span><span class="sxs-lookup"><span data-stu-id="2b605-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="2b605-113">更換 PCM 之前</span><span class="sxs-lookup"><span data-stu-id="2b605-113">Before you replace a PCM</span></span>
<span data-ttu-id="2b605-114">更換 PCM 前，請注意下列重要問題：</span><span class="sxs-lookup"><span data-stu-id="2b605-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="2b605-115">如果 PCM 的電源供應器故障，故障模組請保留不動，但拔掉電源線。</span><span class="sxs-lookup"><span data-stu-id="2b605-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="2b605-116">風扇會繼續從機箱獲得電力，並持續提供適當的冷卻。</span><span class="sxs-lookup"><span data-stu-id="2b605-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="2b605-117">如果風扇故障，必須立刻更換 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="2b605-118">取下 PCM 前，請先中斷 PCM 電力，可關閉主開關 (如果有的話) 或是直接拔掉電源線。</span><span class="sxs-lookup"><span data-stu-id="2b605-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="2b605-119">這是對您的系統發出即將關閉電源的警告。</span><span class="sxs-lookup"><span data-stu-id="2b605-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="2b605-120">取代故障的 PCM 前，請確定其他 PCM 功能正常可供系統持續作業。</span><span class="sxs-lookup"><span data-stu-id="2b605-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="2b605-121">必須盡快以可完全正常運作的 PCM 取代故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="2b605-122">PCM 模組的更換只需要幾分鐘即可完成，但必須在取下故障 PCM 的 10 分鐘內完成以防止過熱。</span><span class="sxs-lookup"><span data-stu-id="2b605-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="2b605-123">請注意，從工廠出貨的替代 764 W PCM 模組將不會包含備用電池模組。</span><span class="sxs-lookup"><span data-stu-id="2b605-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="2b605-124">您在執行替代作業之前，必須先取出故障 PCM 的電池，並將它插入替代模組。</span><span class="sxs-lookup"><span data-stu-id="2b605-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="2b605-125">如需詳細資訊，請參閱如何 [移除並插入備用電池模組](storsimple-battery-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="2b605-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="2b605-126">取下 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-126">Remove a PCM</span></span>
<span data-ttu-id="2b605-127">當您準備好要取下 Microsoft Azure StorSimple 裝置的電源和冷卻模組 (PCM)，請遵循這些指示。</span><span class="sxs-lookup"><span data-stu-id="2b605-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="2b605-128">取下 PCM 之前，請確認您有正確的替代元件 (主要機箱使用764 W，EBOD 機箱使用 580 W)。</span><span class="sxs-lookup"><span data-stu-id="2b605-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="2b605-129">取下 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-129">To remove a PCM</span></span>
1. <span data-ttu-id="2b605-130">在 Azure 傳統入口網站中，按一下 [裝置]  >  [維護]  >  [硬體狀態]。</span><span class="sxs-lookup"><span data-stu-id="2b605-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="2b605-131">檢查 [共用元件]  下 PCM 元件的狀態，找出故障的 PCM：</span><span class="sxs-lookup"><span data-stu-id="2b605-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="2b605-132">如果 PCM 0 的電源供應器故障，[PCM 0 中的電源供應器]  的狀態會變成紅色。</span><span class="sxs-lookup"><span data-stu-id="2b605-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="2b605-133">如果 PCM 1 的電源供應器故障，[PCM 1 中的電源供應器]  的狀態會變成紅色。</span><span class="sxs-lookup"><span data-stu-id="2b605-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="2b605-134">如果 PCM 1 的風扇故障，[PCM 0 的冷卻 0]或 [PCM 0 的冷卻 1] 其中之一的狀態會變成紅色。</span><span class="sxs-lookup"><span data-stu-id="2b605-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="2b605-135">在主要機箱背面找到故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="2b605-136">如果您使用的是 8600 型號，請查看前端面板 LED 顯示器上顯示的「系統單元識別碼」來識別主要機箱。</span><span class="sxs-lookup"><span data-stu-id="2b605-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="2b605-137">主要機箱的預設單位識別碼是 **00**，EBOD 機箱的預設單位識別碼是 **01**。</span><span class="sxs-lookup"><span data-stu-id="2b605-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="2b605-138">下圖和下表說明 LED 顯示器的前端面板。</span><span class="sxs-lookup"><span data-stu-id="2b605-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![前置 OPS 面板上的系統識別碼](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="2b605-140">**圖 1** 裝置的正面面板</span><span class="sxs-lookup"><span data-stu-id="2b605-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="2b605-141">標籤</span><span class="sxs-lookup"><span data-stu-id="2b605-141">Label</span></span> | <span data-ttu-id="2b605-142">說明</span><span class="sxs-lookup"><span data-stu-id="2b605-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2b605-143">1</span><span class="sxs-lookup"><span data-stu-id="2b605-143">1</span></span> |<span data-ttu-id="2b605-144">靜音按鈕</span><span class="sxs-lookup"><span data-stu-id="2b605-144">Mute button</span></span> |
   | <span data-ttu-id="2b605-145">2</span><span class="sxs-lookup"><span data-stu-id="2b605-145">2</span></span> |<span data-ttu-id="2b605-146">系統電源</span><span class="sxs-lookup"><span data-stu-id="2b605-146">System power</span></span> |
   | <span data-ttu-id="2b605-147">3</span><span class="sxs-lookup"><span data-stu-id="2b605-147">3</span></span> |<span data-ttu-id="2b605-148">模組錯誤</span><span class="sxs-lookup"><span data-stu-id="2b605-148">Module fault</span></span> |
   | <span data-ttu-id="2b605-149">4</span><span class="sxs-lookup"><span data-stu-id="2b605-149">4</span></span> |<span data-ttu-id="2b605-150">邏輯錯誤</span><span class="sxs-lookup"><span data-stu-id="2b605-150">Logical fault</span></span> |
   | <span data-ttu-id="2b605-151">5</span><span class="sxs-lookup"><span data-stu-id="2b605-151">5</span></span> |<span data-ttu-id="2b605-152">單元識別碼顯示</span><span class="sxs-lookup"><span data-stu-id="2b605-152">Unit ID display</span></span> |
3. <span data-ttu-id="2b605-153">主要機箱背面的監視 LED 指示燈也可用來識別故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="2b605-154">請看下列圖表以了解如何使用 LED 找出故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="2b605-155">例如，如果對應至 [風扇故障]  的 LED 燈亮了，表示風扇故障。</span><span class="sxs-lookup"><span data-stu-id="2b605-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="2b605-156">同樣的，如果對應至 [AC 故障]  的 LED 燈亮了，表示電源供應器故障。</span><span class="sxs-lookup"><span data-stu-id="2b605-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="2b605-158">**圖 2** PCM 背面和 LED 指示燈</span><span class="sxs-lookup"><span data-stu-id="2b605-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="2b605-159">標籤</span><span class="sxs-lookup"><span data-stu-id="2b605-159">Label</span></span> | <span data-ttu-id="2b605-160">說明</span><span class="sxs-lookup"><span data-stu-id="2b605-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2b605-161">1</span><span class="sxs-lookup"><span data-stu-id="2b605-161">1</span></span> |<span data-ttu-id="2b605-162">AC 電源故障</span><span class="sxs-lookup"><span data-stu-id="2b605-162">AC power failure</span></span> |
   | <span data-ttu-id="2b605-163">2</span><span class="sxs-lookup"><span data-stu-id="2b605-163">2</span></span> |<span data-ttu-id="2b605-164">風扇故障</span><span class="sxs-lookup"><span data-stu-id="2b605-164">Fan failure</span></span> |
   | <span data-ttu-id="2b605-165">3</span><span class="sxs-lookup"><span data-stu-id="2b605-165">3</span></span> |<span data-ttu-id="2b605-166">電池故障</span><span class="sxs-lookup"><span data-stu-id="2b605-166">Battery fault</span></span> |
   | <span data-ttu-id="2b605-167">4</span><span class="sxs-lookup"><span data-stu-id="2b605-167">4</span></span> |<span data-ttu-id="2b605-168">PCM 正常</span><span class="sxs-lookup"><span data-stu-id="2b605-168">PCM OK</span></span> |
   | <span data-ttu-id="2b605-169">5</span><span class="sxs-lookup"><span data-stu-id="2b605-169">5</span></span> |<span data-ttu-id="2b605-170">DC 電源故障</span><span class="sxs-lookup"><span data-stu-id="2b605-170">DC power failure</span></span> |
   | <span data-ttu-id="2b605-171">6</span><span class="sxs-lookup"><span data-stu-id="2b605-171">6</span></span> |<span data-ttu-id="2b605-172">電池狀況良好</span><span class="sxs-lookup"><span data-stu-id="2b605-172">Battery healthy</span></span> |
4. <span data-ttu-id="2b605-173">請看以下的 StorSimple 裝置背面圖，找出故障的 PCM 模組。</span><span class="sxs-lookup"><span data-stu-id="2b605-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="2b605-174">左邊是 PCM 0，右邊是 PCM 1。</span><span class="sxs-lookup"><span data-stu-id="2b605-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="2b605-175">下表說明模組。</span><span class="sxs-lookup"><span data-stu-id="2b605-175">The table that follows explains the modules.</span></span>
   
     ![裝置主要機箱模組的後擋板](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="2b605-177">**圖 3** 裝置背面和外掛程式模組</span><span class="sxs-lookup"><span data-stu-id="2b605-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="2b605-178">標籤</span><span class="sxs-lookup"><span data-stu-id="2b605-178">Label</span></span> | <span data-ttu-id="2b605-179">說明</span><span class="sxs-lookup"><span data-stu-id="2b605-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2b605-180">1</span><span class="sxs-lookup"><span data-stu-id="2b605-180">1</span></span> |<span data-ttu-id="2b605-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="2b605-181">PCM 0</span></span> |
   | <span data-ttu-id="2b605-182">2</span><span class="sxs-lookup"><span data-stu-id="2b605-182">2</span></span> |<span data-ttu-id="2b605-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="2b605-183">PCM 1</span></span> |
   | <span data-ttu-id="2b605-184">3</span><span class="sxs-lookup"><span data-stu-id="2b605-184">3</span></span> |<span data-ttu-id="2b605-185">控制器 0</span><span class="sxs-lookup"><span data-stu-id="2b605-185">Controller 0</span></span> |
   | <span data-ttu-id="2b605-186">4</span><span class="sxs-lookup"><span data-stu-id="2b605-186">4</span></span> |<span data-ttu-id="2b605-187">控制器 1</span><span class="sxs-lookup"><span data-stu-id="2b605-187">Controller 1</span></span> |
5. <span data-ttu-id="2b605-188">關閉故障的 PCM，拔下電源供應器電線。</span><span class="sxs-lookup"><span data-stu-id="2b605-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="2b605-189">您現在可以取下 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="2b605-190">用姆指與食指抓住閂鎖和 PCM 把手的一端，擠壓在一起以開啟把手。</span><span class="sxs-lookup"><span data-stu-id="2b605-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![開啟 PCM 把手](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="2b605-192">**圖 4** 打開 PCM 把手</span><span class="sxs-lookup"><span data-stu-id="2b605-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="2b605-193">抓住把手，取下 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-193">Grip the handle and remove the PCM.</span></span>
   
    ![取下裝置 PCM](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="2b605-195">**圖 5** 取下 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="2b605-196">安裝替代的 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-196">Install a replacement PCM</span></span>
<span data-ttu-id="2b605-197">請遵循這些指示安裝 StorSimple 裝置的 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="2b605-198">請確定您在安裝替代 PCM 之前已經插入備用電池模組 (僅適用 764 W PCM)。</span><span class="sxs-lookup"><span data-stu-id="2b605-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="2b605-199">如需詳細資訊，請參閱如何 [移除並插入備用電池模組](storsimple-battery-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="2b605-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="2b605-200">安裝 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-200">To install a PCM</span></span>
1. <span data-ttu-id="2b605-201">請確認您有這個機箱的正確替代 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="2b605-202">主要機箱需使用 764 W PCM，EBOD 機箱需使用 580 W PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="2b605-203">您不應該嘗試在主要機箱中使用 580 W PCM，或在 EBOD 機箱中使用 764 W PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="2b605-204">下圖顯示貼在 PCM 上的標籤中何處可找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="2b605-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![裝置 PCM 標籤](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="2b605-206">**圖 6** PCM 標籤</span><span class="sxs-lookup"><span data-stu-id="2b605-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="2b605-207">檢查機箱有無損毀，並特別注意接頭。</span><span class="sxs-lookup"><span data-stu-id="2b605-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2b605-208">**如果接頭的任何接腳彎曲，請勿安裝該模組。**</span><span class="sxs-lookup"><span data-stu-id="2b605-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="2b605-209">PCM 把手在開啟的位置，將模組滑入機箱。</span><span class="sxs-lookup"><span data-stu-id="2b605-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![安裝裝置 PCM](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="2b605-211">**圖 7** 安裝 PCM</span><span class="sxs-lookup"><span data-stu-id="2b605-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="2b605-212">手動關閉 PCM 把手。</span><span class="sxs-lookup"><span data-stu-id="2b605-212">Manually close the PCM handle.</span></span> <span data-ttu-id="2b605-213">您應該會聽到喀嚓一聲，表示把手閂鎖已扣上。</span><span class="sxs-lookup"><span data-stu-id="2b605-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2b605-214">若要確保接頭的接腳確實連接，您可以用不會鬆開閂鎖的力道輕拉把手。</span><span class="sxs-lookup"><span data-stu-id="2b605-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="2b605-215">如果 PCM 滑出來，表示接頭連接之前閂鎖就關閉了。</span><span class="sxs-lookup"><span data-stu-id="2b605-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="2b605-216">將電源線插到電力來源和 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="2b605-217">收妥防拉束。</span><span class="sxs-lookup"><span data-stu-id="2b605-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="2b605-218">開啟 PCM。</span><span class="sxs-lookup"><span data-stu-id="2b605-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="2b605-219">確認更換成功：在 StorSimple Manager 服務的 Azure 傳統入口網站中，巡覽至 [裝置]  >  [維護]  >  [硬體狀態]。</span><span class="sxs-lookup"><span data-stu-id="2b605-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="2b605-220">在 [共用元件] 下，PCM 的狀態應該是綠色。</span><span class="sxs-lookup"><span data-stu-id="2b605-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2b605-221">可能需要幾分鐘的時間讓替代的 PCM 完全初始化。</span><span class="sxs-lookup"><span data-stu-id="2b605-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="2b605-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b605-222">Next steps</span></span>
<span data-ttu-id="2b605-223">深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="2b605-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

