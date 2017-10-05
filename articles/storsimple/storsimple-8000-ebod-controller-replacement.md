---
title: "更換 StorSimple 8600 EBOD 控制器 | Microsoft Docs"
description: "說明如何取下並更換 StorSimple 8600 裝置上的一個或兩個 EBOD 控制器。"
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
ms.openlocfilehash: 45699c267d1009c4884dd164fd3f2950d6d5f555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="dcf96-103">更換 StorSimple 裝置上的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="dcf96-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="dcf96-104">概觀</span><span class="sxs-lookup"><span data-stu-id="dcf96-104">Overview</span></span>
<span data-ttu-id="dcf96-105">本教學課程說明如何更換 Microsoft Azure StorSimple 裝置上故障的 EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="dcf96-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="dcf96-106">若要更換 EBOD 控制器模組，您必須：</span><span class="sxs-lookup"><span data-stu-id="dcf96-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="dcf96-107">取下故障的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="dcf96-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="dcf96-108">安裝新的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="dcf96-108">Install a new EBOD controller</span></span>

<span data-ttu-id="dcf96-109">開始之前，請考量下列資訊：</span><span class="sxs-lookup"><span data-stu-id="dcf96-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="dcf96-110">空白的 EBOD 模組必須插入至所有未使用的插槽。</span><span class="sxs-lookup"><span data-stu-id="dcf96-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="dcf96-111">如果插槽處於開啟狀態，機箱將無法適當地冷卻。</span><span class="sxs-lookup"><span data-stu-id="dcf96-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="dcf96-112">EBOD 控制器是可熱交換，而且可以取下或更換。</span><span class="sxs-lookup"><span data-stu-id="dcf96-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="dcf96-113">請勿取下故障的模組，除非您有更換模組。</span><span class="sxs-lookup"><span data-stu-id="dcf96-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="dcf96-114">當起始更換程序時，您必須在 10 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="dcf96-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dcf96-115">在嘗試取下或更換任何 StorSimple 元件之前，請確定先閱讀[安全圖示慣例](storsimple-safety.md#safety-icon-conventions)和其他[安全性預防措施](storsimple-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="dcf96-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="dcf96-116">取下 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="dcf96-116">Remove an EBOD controller</span></span>
<span data-ttu-id="dcf96-117">在取下 StorSimple 裝置中故障的 EBOD 控制器模組之前，請確定另一個 EBOD 控制器模組作用中且執行中。</span><span class="sxs-lookup"><span data-stu-id="dcf96-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="dcf96-118">下列程序和資料表說明如何取下 EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="dcf96-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="dcf96-119">若要取下 EBOD 模組</span><span class="sxs-lookup"><span data-stu-id="dcf96-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="dcf96-120">開啟 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="dcf96-120">Open the Azure portal.</span></span>
2. <span data-ttu-id="dcf96-121">移至您的裝置，並瀏覽至 [設定] > [硬體健康狀態]，並確認作用中 EBOD 控制器模組的 LED 狀態為綠色，而故障的 EBOD 控制器模組的 LED 為紅色。</span><span class="sxs-lookup"><span data-stu-id="dcf96-121">Go to your device and navigate to **Settings** > **Hardware health**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="dcf96-122">在裝置背面找出故障的 EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="dcf96-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="dcf96-123">先取下將 EBOD 控制器模組連接到控制器的纜線，再從系統取出 EBOD 模組。</span><span class="sxs-lookup"><span data-stu-id="dcf96-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="dcf96-124">記下已連接至控制器之 EBOD 控制器模組的確切 SAS 連接埠。</span><span class="sxs-lookup"><span data-stu-id="dcf96-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="dcf96-125">在更換 EBOD 模組之後，您必須將系統還原至這個組態。</span><span class="sxs-lookup"><span data-stu-id="dcf96-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dcf96-126">通常，這將是連接埠 A，在下圖標示為 [主機輸入]。</span><span class="sxs-lookup"><span data-stu-id="dcf96-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   
    ![EBOD 控制器的後擋板](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="dcf96-128">**圖 1** EBOD 模組的背面</span><span class="sxs-lookup"><span data-stu-id="dcf96-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="dcf96-129">標籤</span><span class="sxs-lookup"><span data-stu-id="dcf96-129">Label</span></span> | <span data-ttu-id="dcf96-130">說明</span><span class="sxs-lookup"><span data-stu-id="dcf96-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dcf96-131">1</span><span class="sxs-lookup"><span data-stu-id="dcf96-131">1</span></span> |<span data-ttu-id="dcf96-132">故障 LED</span><span class="sxs-lookup"><span data-stu-id="dcf96-132">Fault LED</span></span> |
   | <span data-ttu-id="dcf96-133">2</span><span class="sxs-lookup"><span data-stu-id="dcf96-133">2</span></span> |<span data-ttu-id="dcf96-134">電源 LED</span><span class="sxs-lookup"><span data-stu-id="dcf96-134">Power LED</span></span> |
   | <span data-ttu-id="dcf96-135">3</span><span class="sxs-lookup"><span data-stu-id="dcf96-135">3</span></span> |<span data-ttu-id="dcf96-136">SAS 連接器</span><span class="sxs-lookup"><span data-stu-id="dcf96-136">SAS connectors</span></span> |
   | <span data-ttu-id="dcf96-137">4</span><span class="sxs-lookup"><span data-stu-id="dcf96-137">4</span></span> |<span data-ttu-id="dcf96-138">SAS LED</span><span class="sxs-lookup"><span data-stu-id="dcf96-138">SAS LEDs</span></span> |
   | <span data-ttu-id="dcf96-139">5</span><span class="sxs-lookup"><span data-stu-id="dcf96-139">5</span></span> |<span data-ttu-id="dcf96-140">僅供原廠使用的序列埠</span><span class="sxs-lookup"><span data-stu-id="dcf96-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="dcf96-141">6</span><span class="sxs-lookup"><span data-stu-id="dcf96-141">6</span></span> |<span data-ttu-id="dcf96-142">連接埠 A (主機輸入)</span><span class="sxs-lookup"><span data-stu-id="dcf96-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="dcf96-143">7</span><span class="sxs-lookup"><span data-stu-id="dcf96-143">7</span></span> |<span data-ttu-id="dcf96-144">連接埠 B (主機輸出)</span><span class="sxs-lookup"><span data-stu-id="dcf96-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="dcf96-145">8</span><span class="sxs-lookup"><span data-stu-id="dcf96-145">8</span></span> |<span data-ttu-id="dcf96-146">連接埠 C (僅限原廠使用)</span><span class="sxs-lookup"><span data-stu-id="dcf96-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="dcf96-147">安裝新的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="dcf96-147">Install a new EBOD controller</span></span>
<span data-ttu-id="dcf96-148">下列程序和資料表說明如何在 StorSimple 中安裝 EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="dcf96-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="dcf96-149">若要安裝新的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="dcf96-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="dcf96-150">請檢查 EBOD 是否損毀，尤其是介面連接器。</span><span class="sxs-lookup"><span data-stu-id="dcf96-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="dcf96-151">如果有任何接腳彎曲，請勿安裝新的 EBOD 控制器。</span><span class="sxs-lookup"><span data-stu-id="dcf96-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="dcf96-152">當閂鎖在開啟的位置時，將模組滑入機箱，直到閂鎖扣上。</span><span class="sxs-lookup"><span data-stu-id="dcf96-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![安裝 EBOD 控制器](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="dcf96-154">**圖 2** 安裝 EBOD 控制器模組</span><span class="sxs-lookup"><span data-stu-id="dcf96-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="dcf96-155">關閉閂鎖。</span><span class="sxs-lookup"><span data-stu-id="dcf96-155">Close the latch.</span></span> <span data-ttu-id="dcf96-156">您應該會聽到喀嚓一聲，表示閂鎖已扣上。</span><span class="sxs-lookup"><span data-stu-id="dcf96-156">You should hear a click as the latch engages.</span></span>
   
    ![鬆開 EBOD 閂鎖](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="dcf96-158">**圖 3** 關閉 EBOD 模組閂鎖</span><span class="sxs-lookup"><span data-stu-id="dcf96-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="dcf96-159">重新連接纜線。</span><span class="sxs-lookup"><span data-stu-id="dcf96-159">Reconnect the cables.</span></span> <span data-ttu-id="dcf96-160">使用更換之前存在的確切組態。</span><span class="sxs-lookup"><span data-stu-id="dcf96-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="dcf96-161">請參閱下圖和資料表，以取得有關如何連接纜線的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dcf96-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![將您的 4U 裝置接上纜線，以取得電源](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="dcf96-163">**圖 4**。</span><span class="sxs-lookup"><span data-stu-id="dcf96-163">**Figure 4**.</span></span> <span data-ttu-id="dcf96-164">重新連接纜線</span><span class="sxs-lookup"><span data-stu-id="dcf96-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="dcf96-165">標籤</span><span class="sxs-lookup"><span data-stu-id="dcf96-165">Label</span></span> | <span data-ttu-id="dcf96-166">說明</span><span class="sxs-lookup"><span data-stu-id="dcf96-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dcf96-167">1</span><span class="sxs-lookup"><span data-stu-id="dcf96-167">1</span></span> |<span data-ttu-id="dcf96-168">主要機箱</span><span class="sxs-lookup"><span data-stu-id="dcf96-168">Primary enclosure</span></span> |
   | <span data-ttu-id="dcf96-169">2</span><span class="sxs-lookup"><span data-stu-id="dcf96-169">2</span></span> |<span data-ttu-id="dcf96-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="dcf96-170">PCM 0</span></span> |
   | <span data-ttu-id="dcf96-171">3</span><span class="sxs-lookup"><span data-stu-id="dcf96-171">3</span></span> |<span data-ttu-id="dcf96-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="dcf96-172">PCM 1</span></span> |
   | <span data-ttu-id="dcf96-173">4</span><span class="sxs-lookup"><span data-stu-id="dcf96-173">4</span></span> |<span data-ttu-id="dcf96-174">控制器 0</span><span class="sxs-lookup"><span data-stu-id="dcf96-174">Controller 0</span></span> |
   | <span data-ttu-id="dcf96-175">5</span><span class="sxs-lookup"><span data-stu-id="dcf96-175">5</span></span> |<span data-ttu-id="dcf96-176">控制器 1</span><span class="sxs-lookup"><span data-stu-id="dcf96-176">Controller 1</span></span> |
   | <span data-ttu-id="dcf96-177">6</span><span class="sxs-lookup"><span data-stu-id="dcf96-177">6</span></span> |<span data-ttu-id="dcf96-178">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="dcf96-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="dcf96-179">7</span><span class="sxs-lookup"><span data-stu-id="dcf96-179">7</span></span> |<span data-ttu-id="dcf96-180">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="dcf96-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="dcf96-181">8</span><span class="sxs-lookup"><span data-stu-id="dcf96-181">8</span></span> |<span data-ttu-id="dcf96-182">EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="dcf96-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="dcf96-183">9</span><span class="sxs-lookup"><span data-stu-id="dcf96-183">9</span></span> |<span data-ttu-id="dcf96-184">電源分配單元</span><span class="sxs-lookup"><span data-stu-id="dcf96-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dcf96-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcf96-185">Next steps</span></span>
<span data-ttu-id="dcf96-186">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="dcf96-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

