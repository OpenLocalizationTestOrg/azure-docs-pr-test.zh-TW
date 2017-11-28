---
title: "aaaReplace StorSimple EBOD 控制器 |Microsoft 文件"
description: "說明如何 tooremove 和取代 StorSimple 8600 裝置上的一個或兩個 EBOD 控制器。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="09e8e-103">更換 StorSimple 裝置上的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="09e8e-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="09e8e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="09e8e-104">Overview</span></span>
<span data-ttu-id="09e8e-105">本教學課程說明如何 tooreplace 上 Microsoft Azure StorSimple 裝置的故障 EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="09e8e-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="09e8e-106">tooreplace EBOD 控制器模組，您要：</span><span class="sxs-lookup"><span data-stu-id="09e8e-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="09e8e-107">移除 hello 故障 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="09e8e-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="09e8e-108">安裝新的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="09e8e-108">Install a new EBOD controller</span></span>

<span data-ttu-id="09e8e-109">請考量下列資訊，在您開始前的 hello:</span><span class="sxs-lookup"><span data-stu-id="09e8e-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="09e8e-110">空白的 EBOD 模組必須插入至所有未使用的插槽。</span><span class="sxs-lookup"><span data-stu-id="09e8e-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="09e8e-111">如果插槽處於開啟狀態，不會正確地冷卻 hello 機箱。</span><span class="sxs-lookup"><span data-stu-id="09e8e-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="09e8e-112">hello EBOD 控制器是可熱交換，可移除或取代。</span><span class="sxs-lookup"><span data-stu-id="09e8e-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="09e8e-113">請勿取下故障的模組，除非您有更換模組。</span><span class="sxs-lookup"><span data-stu-id="09e8e-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="09e8e-114">當您起始 hello 更換程序時，您必須在 10 分鐘內完成它。</span><span class="sxs-lookup"><span data-stu-id="09e8e-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09e8e-115">然後再嘗試 tooremove 或取代任何 StorSimple 元件，請確定您檢閱 hello[安全圖示慣例](storsimple-safety.md#safety-icon-conventions)和其他[安全措施](storsimple-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="09e8e-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="09e8e-116">取下 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="09e8e-116">Remove an EBOD controller</span></span>
<span data-ttu-id="09e8e-117">取代 hello 失敗 EBOD 控制器模組在您的 StorSimple 裝置，請確定該 hello 其他 EBOD 控制器模組已使用中且正在執行。</span><span class="sxs-lookup"><span data-stu-id="09e8e-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="09e8e-118">hello 下列程序及下表說明如何 tooremove hello EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="09e8e-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="09e8e-119">tooremove EBOD 模組</span><span class="sxs-lookup"><span data-stu-id="09e8e-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="09e8e-120">開啟 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="09e8e-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="09e8e-121">瀏覽過**裝置** > **維護** > **硬體狀態**，並確認 hello hello 狀態 LED 的 hello active EBOD控制器模組為綠色，而失敗的 hello EBOD 控制器模組的 hello LED 為紅色。</span><span class="sxs-lookup"><span data-stu-id="09e8e-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="09e8e-122">在 hello hello 裝置背面尋找失敗的 hello EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="09e8e-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="09e8e-123">移除 hello 連接纜線，hello EBOD 控制器模組 toohello 控制器再超出 hello 系統 hello EBOD 模組。</span><span class="sxs-lookup"><span data-stu-id="09e8e-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="09e8e-124">記下 hello 確切 SAS 連接埠已連接的 toohello 控制站的 hello EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="09e8e-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="09e8e-125">取代 hello EBOD 模組之後，您將會需要的 toorestore hello 系統 toothis 組態。</span><span class="sxs-lookup"><span data-stu-id="09e8e-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="09e8e-126">一般來說，這將是連接埠 A，標示為**中裝載**hello 下列圖表中。</span><span class="sxs-lookup"><span data-stu-id="09e8e-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![EBOD 控制器的後擋板](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="09e8e-128">**圖 1** EBOD 模組的背面</span><span class="sxs-lookup"><span data-stu-id="09e8e-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="09e8e-129">標籤</span><span class="sxs-lookup"><span data-stu-id="09e8e-129">Label</span></span> | <span data-ttu-id="09e8e-130">說明</span><span class="sxs-lookup"><span data-stu-id="09e8e-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="09e8e-131">1</span><span class="sxs-lookup"><span data-stu-id="09e8e-131">1</span></span> |<span data-ttu-id="09e8e-132">故障 LED</span><span class="sxs-lookup"><span data-stu-id="09e8e-132">Fault LED</span></span> |
   | <span data-ttu-id="09e8e-133">2</span><span class="sxs-lookup"><span data-stu-id="09e8e-133">2</span></span> |<span data-ttu-id="09e8e-134">電源 LED</span><span class="sxs-lookup"><span data-stu-id="09e8e-134">Power LED</span></span> |
   | <span data-ttu-id="09e8e-135">3</span><span class="sxs-lookup"><span data-stu-id="09e8e-135">3</span></span> |<span data-ttu-id="09e8e-136">SAS 連接器</span><span class="sxs-lookup"><span data-stu-id="09e8e-136">SAS connectors</span></span> |
   | <span data-ttu-id="09e8e-137">4</span><span class="sxs-lookup"><span data-stu-id="09e8e-137">4</span></span> |<span data-ttu-id="09e8e-138">SAS LED</span><span class="sxs-lookup"><span data-stu-id="09e8e-138">SAS LEDs</span></span> |
   | <span data-ttu-id="09e8e-139">5</span><span class="sxs-lookup"><span data-stu-id="09e8e-139">5</span></span> |<span data-ttu-id="09e8e-140">僅供原廠使用的序列埠</span><span class="sxs-lookup"><span data-stu-id="09e8e-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="09e8e-141">6</span><span class="sxs-lookup"><span data-stu-id="09e8e-141">6</span></span> |<span data-ttu-id="09e8e-142">連接埠 A (主機輸入)</span><span class="sxs-lookup"><span data-stu-id="09e8e-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="09e8e-143">7</span><span class="sxs-lookup"><span data-stu-id="09e8e-143">7</span></span> |<span data-ttu-id="09e8e-144">連接埠 B (主機輸出)</span><span class="sxs-lookup"><span data-stu-id="09e8e-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="09e8e-145">8</span><span class="sxs-lookup"><span data-stu-id="09e8e-145">8</span></span> |<span data-ttu-id="09e8e-146">連接埠 C (僅限原廠使用)</span><span class="sxs-lookup"><span data-stu-id="09e8e-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="09e8e-147">安裝新的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="09e8e-147">Install a new EBOD controller</span></span>
<span data-ttu-id="09e8e-148">hello 下列程序及下表說明如何 tooinstall EBOD 控制器模組在您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="09e8e-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="09e8e-149">tooinstall EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="09e8e-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="09e8e-150">請檢查有無損壞，特別是 toohello 介面連接器 hello EBOD 裝置。</span><span class="sxs-lookup"><span data-stu-id="09e8e-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="09e8e-151">如果有任何彎曲的插腳，請勿安裝 hello 新 EBOD 控制器。</span><span class="sxs-lookup"><span data-stu-id="09e8e-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="09e8e-152">Hello 閂鎖在 hello 與開啟投影片 hello hello 閂鎖嚙合之前的 hello 機箱模組的位置。</span><span class="sxs-lookup"><span data-stu-id="09e8e-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![安裝 EBOD 控制器](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="09e8e-154">**圖 2**安裝 hello EBOD 控制器模組</span><span class="sxs-lookup"><span data-stu-id="09e8e-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="09e8e-155">關閉 hello 閂鎖。</span><span class="sxs-lookup"><span data-stu-id="09e8e-155">Close hello latch.</span></span> <span data-ttu-id="09e8e-156">您應該為 hello 閂鎖嚙合時聽到喀。</span><span class="sxs-lookup"><span data-stu-id="09e8e-156">You should hear a click as hello latch engages.</span></span>
   
    ![鬆開 EBOD 閂鎖](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="09e8e-158">**圖 3**關閉 hello EBOD 模組閂鎖</span><span class="sxs-lookup"><span data-stu-id="09e8e-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="09e8e-159">重新連線 hello 纜線。</span><span class="sxs-lookup"><span data-stu-id="09e8e-159">Reconnect hello cables.</span></span> <span data-ttu-id="09e8e-160">使用 hello hello 更換前出現的確切組態。</span><span class="sxs-lookup"><span data-stu-id="09e8e-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="09e8e-161">請參閱下列圖表中的 hello 和資料表的詳細說明如何 tooconnect hello 纜線。</span><span class="sxs-lookup"><span data-stu-id="09e8e-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![將您的 4U 裝置接上纜線，以取得電源](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="09e8e-163">**圖 4**。</span><span class="sxs-lookup"><span data-stu-id="09e8e-163">**Figure 4**.</span></span> <span data-ttu-id="09e8e-164">重新連接纜線</span><span class="sxs-lookup"><span data-stu-id="09e8e-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="09e8e-165">標籤</span><span class="sxs-lookup"><span data-stu-id="09e8e-165">Label</span></span> | <span data-ttu-id="09e8e-166">說明</span><span class="sxs-lookup"><span data-stu-id="09e8e-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="09e8e-167">1</span><span class="sxs-lookup"><span data-stu-id="09e8e-167">1</span></span> |<span data-ttu-id="09e8e-168">主要機箱</span><span class="sxs-lookup"><span data-stu-id="09e8e-168">Primary enclosure</span></span> |
   | <span data-ttu-id="09e8e-169">2</span><span class="sxs-lookup"><span data-stu-id="09e8e-169">2</span></span> |<span data-ttu-id="09e8e-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="09e8e-170">PCM 0</span></span> |
   | <span data-ttu-id="09e8e-171">3</span><span class="sxs-lookup"><span data-stu-id="09e8e-171">3</span></span> |<span data-ttu-id="09e8e-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="09e8e-172">PCM 1</span></span> |
   | <span data-ttu-id="09e8e-173">4</span><span class="sxs-lookup"><span data-stu-id="09e8e-173">4</span></span> |<span data-ttu-id="09e8e-174">控制器 0</span><span class="sxs-lookup"><span data-stu-id="09e8e-174">Controller 0</span></span> |
   | <span data-ttu-id="09e8e-175">5</span><span class="sxs-lookup"><span data-stu-id="09e8e-175">5</span></span> |<span data-ttu-id="09e8e-176">控制器 1</span><span class="sxs-lookup"><span data-stu-id="09e8e-176">Controller 1</span></span> |
   | <span data-ttu-id="09e8e-177">6</span><span class="sxs-lookup"><span data-stu-id="09e8e-177">6</span></span> |<span data-ttu-id="09e8e-178">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="09e8e-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="09e8e-179">7</span><span class="sxs-lookup"><span data-stu-id="09e8e-179">7</span></span> |<span data-ttu-id="09e8e-180">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="09e8e-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="09e8e-181">8</span><span class="sxs-lookup"><span data-stu-id="09e8e-181">8</span></span> |<span data-ttu-id="09e8e-182">EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="09e8e-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="09e8e-183">9</span><span class="sxs-lookup"><span data-stu-id="09e8e-183">9</span></span> |<span data-ttu-id="09e8e-184">電源分配單元</span><span class="sxs-lookup"><span data-stu-id="09e8e-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="09e8e-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09e8e-185">Next steps</span></span>
<span data-ttu-id="09e8e-186">深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="09e8e-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

