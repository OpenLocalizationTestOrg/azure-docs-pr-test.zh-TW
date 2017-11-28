---
title: "在您的 StorSimple 8000 系列裝置 PCM aaaReplace |Microsoft 文件"
description: "說明如何 tooremove 和取代 hello 電源和冷卻模組 (PCM) 上您的 StorSimple 裝置"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="fae38-103">更換 StorSimple 裝置上的電源和冷卻模組</span><span class="sxs-lookup"><span data-stu-id="fae38-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="fae38-104">概觀</span><span class="sxs-lookup"><span data-stu-id="fae38-104">Overview</span></span>
<span data-ttu-id="fae38-105">hello 電源和冷卻模組 (PCM) 您的 Microsoft Azure StorSimple 裝置中包含的電源供應器和冷卻風扇控制透過 hello 主要和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="fae38-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="fae38-106">每個機箱只有一個認證的 PCM 模型。</span><span class="sxs-lookup"><span data-stu-id="fae38-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="fae38-107">764 W PCM hello 主要機箱已通過認證，而且 hello EBOD 機箱都通過認證 580 W PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="fae38-108">雖然主要機箱 hello 和 hello EBOD 機箱的 Pcm hello 不同，但 hello 更換程序是完全相同。</span><span class="sxs-lookup"><span data-stu-id="fae38-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="fae38-109">本教學課程說明如何：</span><span class="sxs-lookup"><span data-stu-id="fae38-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="fae38-110">取下 PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-110">Remove a PCM</span></span>
* <span data-ttu-id="fae38-111">安裝替代的 PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fae38-112">移除和更換 PCM，檢閱中的 hello 安全性資訊之前[StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="fae38-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="fae38-113">更換 PCM 之前</span><span class="sxs-lookup"><span data-stu-id="fae38-113">Before you replace a PCM</span></span>
<span data-ttu-id="fae38-114">請注意下列重要問題，在更換 PCM 之前 hello:</span><span class="sxs-lookup"><span data-stu-id="fae38-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="fae38-115">如果 hello 電源供應器的 hello PCM 故障，讓 hello 安裝，故障的模組，但移除 hello 電源線。</span><span class="sxs-lookup"><span data-stu-id="fae38-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="fae38-116">hello 風扇會繼續 tooreceive hello 機箱電源，並繼續 tooprovide 適當冷卻。</span><span class="sxs-lookup"><span data-stu-id="fae38-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="fae38-117">如果 hello 風扇故障，hello PCM 必須立即卸下 toobe。</span><span class="sxs-lookup"><span data-stu-id="fae38-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="fae38-118">然後再移除 hello PCM，hello 電源中斷 hello PCM，關閉 hello 主開關 （若有的話） 或實際拔 hello 電源線。</span><span class="sxs-lookup"><span data-stu-id="fae38-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="fae38-119">這提供警告 tooyour 系統，即將關閉電源。</span><span class="sxs-lookup"><span data-stu-id="fae38-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="fae38-120">請確定其他 PCM 正常運作的該 hello 繼續系統作業之前取代 hello 故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="fae38-121">必須盡快以可完全正常運作的 PCM 取代故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="fae38-122">更換 PCM 模組會採用只有幾分鐘的時間 toocomplete，但它必須移除失敗的 hello PCM tooprevent 過熱的 10 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="fae38-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="fae38-123">請注意 hello 取代 764 W PCM 模組從 hello 原廠出貨不包含 hello 備用電池模組。</span><span class="sxs-lookup"><span data-stu-id="fae38-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="fae38-124">您將需要 tooremove hello 電池故障的 PCM，然後再將它插入 hello 取代模組先前 tooperforming hello 更換。</span><span class="sxs-lookup"><span data-stu-id="fae38-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="fae38-125">如需詳細資訊，請參閱如何太[移除並插入備份電池模組](storsimple-8000-battery-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="fae38-125">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="fae38-126">取下 PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-126">Remove a PCM</span></span>
<span data-ttu-id="fae38-127">當您準備 tooremove 電源和冷卻模組 (PCM) 從 Microsoft Azure StorSimple 裝置，請遵循這些指示。</span><span class="sxs-lookup"><span data-stu-id="fae38-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="fae38-128">移除 PCM 之前，請確認您有正確的替換 (764 W 適用於主要機箱 hello) 或 580 W 適用於 hello EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="fae38-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="fae38-129">tooremove PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-129">tooremove a PCM</span></span>
1. <span data-ttu-id="fae38-130">在 hello Azure 傳統入口網站，按一下 **設定 > 監視 > 硬體健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="fae38-130">In hello Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="fae38-131">檢查 hello hello 之下 PCM 元件狀態**共用元件**tooidentify 哪個 PCM 已故障：</span><span class="sxs-lookup"><span data-stu-id="fae38-131">Check hello status of hello PCM components under **Shared components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="fae38-132">如果 PCM 0 中的電源供應器故障，hello 狀態**PCM 0 中的電源供應器**會變成紅色。</span><span class="sxs-lookup"><span data-stu-id="fae38-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="fae38-133">如果 PCM 1 中的電源供應器故障，hello 狀態**PCM 1 中的電源供應器**會變成紅色。</span><span class="sxs-lookup"><span data-stu-id="fae38-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="fae38-134">如果 PCM 1 中的 hello 風扇故障，hello 狀態中的其中一個**PCM 0 的冷卻 0**或**PCM 0 的冷卻 1**會變成紅色。</span><span class="sxs-lookup"><span data-stu-id="fae38-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="fae38-135">找出故障的 PCM 上 hello 回 hello 主要機箱的 hello。</span><span class="sxs-lookup"><span data-stu-id="fae38-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="fae38-136">如果您正在 8600 模型，請查看 hello 系統單元識別碼 hello 前端面板 LED 顯示器上顯示識別 hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="fae38-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="fae38-137">hello 的預設單元識別碼 hello 主要機箱上顯示為**00**，而 hello 預設單元識別碼 hello EBOD 機箱顯示為**01**。</span><span class="sxs-lookup"><span data-stu-id="fae38-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="fae38-138">hello 下列圖表說明 hello LED 顯示 hello 前端面板。</span><span class="sxs-lookup"><span data-stu-id="fae38-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![前置 OPS 面板上的系統識別碼](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="fae38-140">**圖 1** hello 裝置的前面板</span><span class="sxs-lookup"><span data-stu-id="fae38-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="fae38-141">標籤</span><span class="sxs-lookup"><span data-stu-id="fae38-141">Label</span></span> | <span data-ttu-id="fae38-142">說明</span><span class="sxs-lookup"><span data-stu-id="fae38-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fae38-143">1</span><span class="sxs-lookup"><span data-stu-id="fae38-143">1</span></span> |<span data-ttu-id="fae38-144">靜音按鈕</span><span class="sxs-lookup"><span data-stu-id="fae38-144">Mute button</span></span> |
   | <span data-ttu-id="fae38-145">2</span><span class="sxs-lookup"><span data-stu-id="fae38-145">2</span></span> |<span data-ttu-id="fae38-146">系統電源</span><span class="sxs-lookup"><span data-stu-id="fae38-146">System power</span></span> |
   | <span data-ttu-id="fae38-147">3</span><span class="sxs-lookup"><span data-stu-id="fae38-147">3</span></span> |<span data-ttu-id="fae38-148">模組錯誤</span><span class="sxs-lookup"><span data-stu-id="fae38-148">Module fault</span></span> |
   | <span data-ttu-id="fae38-149">4</span><span class="sxs-lookup"><span data-stu-id="fae38-149">4</span></span> |<span data-ttu-id="fae38-150">邏輯錯誤</span><span class="sxs-lookup"><span data-stu-id="fae38-150">Logical fault</span></span> |
   | <span data-ttu-id="fae38-151">5</span><span class="sxs-lookup"><span data-stu-id="fae38-151">5</span></span> |<span data-ttu-id="fae38-152">單元識別碼顯示</span><span class="sxs-lookup"><span data-stu-id="fae38-152">Unit ID display</span></span> |
3. <span data-ttu-id="fae38-153">也可以使用監控指示器 Led hello 主要機箱背面的 hello 中的 hello tooidentify hello 故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="fae38-154">請參閱 hello 下列圖表，以及如何資料表 toounderstand toouse hello Led toolocate hello 故障的 PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="fae38-155">例如，如果 hello 導致對應 toohello**風扇故障**會亮起，風扇 hello 已故障。</span><span class="sxs-lookup"><span data-stu-id="fae38-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="fae38-156">同樣地，如果 hello 造成太對應**AC 故障**會亮起，hello 電源供應器已故障。</span><span class="sxs-lookup"><span data-stu-id="fae38-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![裝置後擋板 PCM 監視 LED 指示燈](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="fae38-158">**圖 2** PCM 背面和 LED 指示燈</span><span class="sxs-lookup"><span data-stu-id="fae38-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="fae38-159">標籤</span><span class="sxs-lookup"><span data-stu-id="fae38-159">Label</span></span> | <span data-ttu-id="fae38-160">說明</span><span class="sxs-lookup"><span data-stu-id="fae38-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fae38-161">1</span><span class="sxs-lookup"><span data-stu-id="fae38-161">1</span></span> |<span data-ttu-id="fae38-162">AC 電源故障</span><span class="sxs-lookup"><span data-stu-id="fae38-162">AC power failure</span></span> |
   | <span data-ttu-id="fae38-163">2</span><span class="sxs-lookup"><span data-stu-id="fae38-163">2</span></span> |<span data-ttu-id="fae38-164">風扇故障</span><span class="sxs-lookup"><span data-stu-id="fae38-164">Fan failure</span></span> |
   | <span data-ttu-id="fae38-165">3</span><span class="sxs-lookup"><span data-stu-id="fae38-165">3</span></span> |<span data-ttu-id="fae38-166">電池故障</span><span class="sxs-lookup"><span data-stu-id="fae38-166">Battery fault</span></span> |
   | <span data-ttu-id="fae38-167">4</span><span class="sxs-lookup"><span data-stu-id="fae38-167">4</span></span> |<span data-ttu-id="fae38-168">PCM 正常</span><span class="sxs-lookup"><span data-stu-id="fae38-168">PCM OK</span></span> |
   | <span data-ttu-id="fae38-169">5</span><span class="sxs-lookup"><span data-stu-id="fae38-169">5</span></span> |<span data-ttu-id="fae38-170">DC 電源故障</span><span class="sxs-lookup"><span data-stu-id="fae38-170">DC power failure</span></span> |
   | <span data-ttu-id="fae38-171">6</span><span class="sxs-lookup"><span data-stu-id="fae38-171">6</span></span> |<span data-ttu-id="fae38-172">電池狀況良好</span><span class="sxs-lookup"><span data-stu-id="fae38-172">Battery healthy</span></span> |
4. <span data-ttu-id="fae38-173">請參閱 toohello 遵循 hello hello StorSimple 裝置 toolocate hello 失敗 PCM 模組的背面的圖表。</span><span class="sxs-lookup"><span data-stu-id="fae38-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="fae38-174">PCM 0 位於左邊 hello 和 PCM 1 位於右邊 hello。</span><span class="sxs-lookup"><span data-stu-id="fae38-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="fae38-175">hello 表會說明 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="fae38-175">hello table that follows explains hello modules.</span></span>
   
     ![裝置主要機箱模組的後擋板](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="fae38-177">**圖 3** 裝置背面和外掛程式模組</span><span class="sxs-lookup"><span data-stu-id="fae38-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="fae38-178">標籤</span><span class="sxs-lookup"><span data-stu-id="fae38-178">Label</span></span> | <span data-ttu-id="fae38-179">說明</span><span class="sxs-lookup"><span data-stu-id="fae38-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fae38-180">1</span><span class="sxs-lookup"><span data-stu-id="fae38-180">1</span></span> |<span data-ttu-id="fae38-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="fae38-181">PCM 0</span></span> |
   | <span data-ttu-id="fae38-182">2</span><span class="sxs-lookup"><span data-stu-id="fae38-182">2</span></span> |<span data-ttu-id="fae38-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="fae38-183">PCM 1</span></span> |
   | <span data-ttu-id="fae38-184">3</span><span class="sxs-lookup"><span data-stu-id="fae38-184">3</span></span> |<span data-ttu-id="fae38-185">控制器 0</span><span class="sxs-lookup"><span data-stu-id="fae38-185">Controller 0</span></span> |
   | <span data-ttu-id="fae38-186">4</span><span class="sxs-lookup"><span data-stu-id="fae38-186">4</span></span> |<span data-ttu-id="fae38-187">控制器 1</span><span class="sxs-lookup"><span data-stu-id="fae38-187">Controller 1</span></span> |
5. <span data-ttu-id="fae38-188">開啟關閉 hello 故障的 PCM 並中斷連線 hello 電源線。</span><span class="sxs-lookup"><span data-stu-id="fae38-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="fae38-189">您現在可以移除 hello PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="fae38-190">Hello 閂鎖和 hello 側邊的 hello PCM 處理姆指與食指，並將其緊壓在一起的 tooopen hello 控制代碼。</span><span class="sxs-lookup"><span data-stu-id="fae38-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![開啟 PCM 把手](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="fae38-192">**圖 4**開啟 hello PCM 處理</span><span class="sxs-lookup"><span data-stu-id="fae38-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="fae38-193">底框 hello 處理，並移除 hello PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![取下裝置 PCM](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="fae38-195">**圖 5**移除 hello PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="fae38-196">安裝替代的 PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-196">Install a replacement PCM</span></span>
<span data-ttu-id="fae38-197">請遵循這些指示 tooinstall StorSimple 裝置中的 PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="fae38-198">請確定您已插入 hello 備用電池模組先前 tooinstalling hello 替換 PCM （適用於僅 too764 W Pcm）。</span><span class="sxs-lookup"><span data-stu-id="fae38-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="fae38-199">如需詳細資訊，請參閱如何太[移除並插入備份電池模組](storsimple-8000-battery-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="fae38-199">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="fae38-200">tooinstall PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="fae38-201">確認您擁有 hello 正確替換 PCM，這個機箱。</span><span class="sxs-lookup"><span data-stu-id="fae38-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="fae38-202">hello 主要機箱需要 764 W PCM，而 hello EBOD 機箱則需要 580 W PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="fae38-203">您不應嘗試 toouse hello 580 W PCM hello 主要機箱中的或 hello 764 W PCM hello EBOD 機箱中的。</span><span class="sxs-lookup"><span data-stu-id="fae38-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="fae38-204">下列影像顯示其中 tooidentify hello 此資訊也就是加上標籤貼附 toohello PCM hello。</span><span class="sxs-lookup"><span data-stu-id="fae38-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![裝置 PCM 標籤](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="fae38-206">**圖 6** PCM 標籤</span><span class="sxs-lookup"><span data-stu-id="fae38-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="fae38-207">檢查有損毀 toohello 機箱，應特別注意 toohello 連接器。</span><span class="sxs-lookup"><span data-stu-id="fae38-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fae38-208">**如果任何連接器插腳，請勿安裝 hello 模組。**</span><span class="sxs-lookup"><span data-stu-id="fae38-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="fae38-209">以 hello PCM 處理 hello 中開啟投影片 hello hello 機箱模組的位置。</span><span class="sxs-lookup"><span data-stu-id="fae38-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![安裝裝置 PCM](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="fae38-211">**圖 7**安裝 hello PCM</span><span class="sxs-lookup"><span data-stu-id="fae38-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="fae38-212">手動關閉 hello PCM 把手。</span><span class="sxs-lookup"><span data-stu-id="fae38-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="fae38-213">您應該為 hello 把手閂鎖嚙合時聽到喀。</span><span class="sxs-lookup"><span data-stu-id="fae38-213">You should hear a click as hello handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fae38-214">hello 的連接器已嚙合，您可以輕輕 tug hello 控制代碼上，但未釋放 hello 閂鎖的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="fae38-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="fae38-215">如果 hello PCM 滑出，則表示該 hello 閂鎖 hello 連接器嚙合之前關閉。</span><span class="sxs-lookup"><span data-stu-id="fae38-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   
5. <span data-ttu-id="fae38-216">Hello 電源纜線 toohello 電源和 toohello PCM 連接。</span><span class="sxs-lookup"><span data-stu-id="fae38-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="fae38-217">浮雕 bales 安全 hello 疲勞。</span><span class="sxs-lookup"><span data-stu-id="fae38-217">Secure hello strain relief bales.</span></span>
7. <span data-ttu-id="fae38-218">開啟 hello PCM。</span><span class="sxs-lookup"><span data-stu-id="fae38-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="fae38-219">確認已順利 hello 更換： hello Azure 入口網站，您的 StorSimple 裝置管理員服務，在瀏覽 tooyour 裝置，然後太**設定 > 監視 > 硬體健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="fae38-219">Verify that hello replacement was successful: in hello Azure portal of your StorSimple Device Manager service, navigate tooyour device and then too**Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="fae38-220">在 hello**共用元件**，hello 的 hello PCM 的狀態應為綠色。</span><span class="sxs-lookup"><span data-stu-id="fae38-220">Under hello **Shared components**, hello status of hello PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fae38-221">可能需要幾分鐘，讓 hello 更換 PCM toocompletely 初始化。</span><span class="sxs-lookup"><span data-stu-id="fae38-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fae38-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fae38-222">Next steps</span></span>
<span data-ttu-id="fae38-223">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="fae38-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

