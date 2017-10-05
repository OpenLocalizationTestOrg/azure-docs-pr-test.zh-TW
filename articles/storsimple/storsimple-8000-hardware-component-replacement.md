---
title: "StorSimple 8000 系列硬體元件更換 | Microsoft Docs"
description: "說明如何安全地更換 PCM、電池、控制器模組、EBOD 控制器、磁碟機，以及 StorSimple 裝置底座。"
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
ms.custom: 
ms.openlocfilehash: 6de50c5031db59176bdf17ecc69b934559220f6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a><span data-ttu-id="cf73d-103">更換 StorSimple 8000 系列裝置上的硬體元件</span><span class="sxs-lookup"><span data-stu-id="cf73d-103">Replace a hardware component on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="cf73d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cf73d-104">Overview</span></span>
<span data-ttu-id="cf73d-105">硬體元件更換教學課程將說明 Microsoft Azure StorSimple 8000 系列裝置的硬體元件，以及取下並更換這些元件所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="cf73d-105">The hardware component replacement tutorials describe the hardware components of your Microsoft Azure StorSimple 8000 series device and the steps necessary to remove and replace them.</span></span> <span data-ttu-id="cf73d-106">本文說明安全圖示、提供詳細教學課程的重點，並列出可替換的元件。</span><span class="sxs-lookup"><span data-stu-id="cf73d-106">This article describes the safety icons, provides pointers to the detailed tutorials, and lists the components that are replaceable.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf73d-107">在嘗試取下或更換任何 StorSimple 元件之前，請確定先閱讀[安全圖示慣例](#safety-icon-conventions)和其他[安全性預防措施](storsimple-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="cf73d-107">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>


### <a name="safety-icon-conventions"></a><span data-ttu-id="cf73d-108">安全性圖示慣例</span><span class="sxs-lookup"><span data-stu-id="cf73d-108">Safety icon conventions</span></span>
<span data-ttu-id="cf73d-109">下表說明本教學課程中使用的安全性圖示。</span><span class="sxs-lookup"><span data-stu-id="cf73d-109">The following table describes the safety icons used in these tutorials.</span></span> <span data-ttu-id="cf73d-110">當您瀏覽取下並更換裝置元件的步驟時，請密切注意這些安全性圖示。</span><span class="sxs-lookup"><span data-stu-id="cf73d-110">Pay close attention to these safety icons as you go through the steps to remove and replace device components.</span></span>

| <span data-ttu-id="cf73d-111">圖示</span><span class="sxs-lookup"><span data-stu-id="cf73d-111">Icon</span></span> | <span data-ttu-id="cf73d-112">文字</span><span class="sxs-lookup"><span data-stu-id="cf73d-112">Text</span></span> | <span data-ttu-id="cf73d-113">其他資訊</span><span class="sxs-lookup"><span data-stu-id="cf73d-113">Additional information</span></span> |
|:--- |:--- |:--- |
| ![警告圖示](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="cf73d-115">**危險！**</span><span class="sxs-lookup"><span data-stu-id="cf73d-115">**DANGER!**</span></span> |<span data-ttu-id="cf73d-116">指出危險的情況，如果無法避免，將會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="cf73d-116">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="cf73d-117">此訊號文字僅限用於最極端的情況。</span><span class="sxs-lookup"><span data-stu-id="cf73d-117">This signal word is limited to the most extreme situations.</span></span> |
| ![警告圖示](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="cf73d-119">**警告！**</span><span class="sxs-lookup"><span data-stu-id="cf73d-119">**WARNING!**</span></span> |<span data-ttu-id="cf73d-120">指出危險的情況，如果無法避免，可能會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="cf73d-120">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| ![注意圖示](./media/storsimple-hardware-component-replacement/Caution.png) |<span data-ttu-id="cf73d-122">**小心！**</span><span class="sxs-lookup"><span data-stu-id="cf73d-122">**CAUTION!**</span></span> |<span data-ttu-id="cf73d-123">指出危險的情況，如果無法避免，可能會導致次要或中度的傷害。</span><span class="sxs-lookup"><span data-stu-id="cf73d-123">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| ![注意事項圖示](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |<span data-ttu-id="cf73d-125">**注意事項：**</span><span class="sxs-lookup"><span data-stu-id="cf73d-125">**NOTICE:**</span></span> |<span data-ttu-id="cf73d-126">表示重要資訊，但與危險無關。</span><span class="sxs-lookup"><span data-stu-id="cf73d-126">Indicates information considered important, but not hazard-related.</span></span> |
| ![電擊圖示](./media/storsimple-hardware-component-replacement/Electric.png) |<span data-ttu-id="cf73d-128">**電擊危險**</span><span class="sxs-lookup"><span data-stu-id="cf73d-128">**Electrical Shock Hazard**</span></span> |<span data-ttu-id="cf73d-129">表示高電壓。</span><span class="sxs-lookup"><span data-stu-id="cf73d-129">Indicates high voltage.</span></span> |
| ![超重圖示](./media/storsimple-hardware-component-replacement/Weight.png) |<span data-ttu-id="cf73d-131">**超重**</span><span class="sxs-lookup"><span data-stu-id="cf73d-131">**Heavy Weight**</span></span> | |
| ![沒有使用者可自行維修的零件圖示](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |<span data-ttu-id="cf73d-133">**沒有使用者可自行維修的零件**</span><span class="sxs-lookup"><span data-stu-id="cf73d-133">**No User Serviceable Parts**</span></span> |<span data-ttu-id="cf73d-134">除非受過適當訓練，否則請勿觸碰。</span><span class="sxs-lookup"><span data-stu-id="cf73d-134">Do not access unless properly trained.</span></span> |
| ![閱讀指示圖示](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |<span data-ttu-id="cf73d-136">**請先閱讀所有指示**</span><span class="sxs-lookup"><span data-stu-id="cf73d-136">**Read All Instructions First**</span></span> | |
| ![傾倒危險圖示](./media/storsimple-hardware-component-replacement/TipHazard.png) |<span data-ttu-id="cf73d-138">**傾倒危險**</span><span class="sxs-lookup"><span data-stu-id="cf73d-138">**Tip Hazard**</span></span> | |

### <a name="before-you-begin"></a><span data-ttu-id="cf73d-139">開始之前</span><span class="sxs-lookup"><span data-stu-id="cf73d-139">Before you begin</span></span>
<span data-ttu-id="cf73d-140">讓您自己熟悉有關裝置的安全性資訊，以及本教學課程中使用的安全性圖示。</span><span class="sxs-lookup"><span data-stu-id="cf73d-140">Familiarize yourself with the safety information about your device and safety icons used in this tutorial.</span></span> <span data-ttu-id="cf73d-141">如需完整資訊，請移至 [安全地安裝和操作您的 StorSimple 裝置](storsimple-safety.md) 。</span><span class="sxs-lookup"><span data-stu-id="cf73d-141">Go to [Safely install and operate your StorSimple device](storsimple-safety.md) for complete information.</span></span> <span data-ttu-id="cf73d-142">請務必閱讀 [安全性預防措施](storsimple-safety.md#handling-precautions) ，然後再處理 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="cf73d-142">Be sure to review the [Safety precautions](storsimple-safety.md#handling-precautions) before you handle your StorSimple device.</span></span>

<span data-ttu-id="cf73d-143">在嘗試更換元件之前，請考量下列資訊。</span><span class="sxs-lookup"><span data-stu-id="cf73d-143">Before you attempt to replace a component, consider the following information.</span></span>

<span data-ttu-id="cf73d-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="cf73d-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **WARNING!**</span></span>

* <span data-ttu-id="cf73d-145">處理 StorSimple 裝置的模組和元件時，請使用靜電防護或防靜電墊，讓您自己適當地接地。</span><span class="sxs-lookup"><span data-stu-id="cf73d-145">Ground yourself properly by using an electrostatic discharge or antistatic mat when handling modules and components of your StorSimple device.</span></span>
* <span data-ttu-id="cf73d-146">請勿觸及任何電路。</span><span class="sxs-lookup"><span data-stu-id="cf73d-146">Do not touch any circuitry.</span></span> <span data-ttu-id="cf73d-147">在處理可能曝露電路的元件時，請使用提供的把手和導路。</span><span class="sxs-lookup"><span data-stu-id="cf73d-147">Use the supplied handles and guides while handling components that may have exposed circuitry.</span></span>

<span data-ttu-id="cf73d-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="cf73d-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **NOTICE:**</span></span>

<span data-ttu-id="cf73d-149">當更換模組時， **決不在機箱背面留下空白機架**。</span><span class="sxs-lookup"><span data-stu-id="cf73d-149">When you replace a module, **NEVER leave an empty bay in the rear of the enclosure**.</span></span> <span data-ttu-id="cf73d-150">在取下問題組件之前，請取得更換或空白模組。</span><span class="sxs-lookup"><span data-stu-id="cf73d-150">Obtain a replacement or blank module before removing the problem part.</span></span>

## <a name="hardware-component-replacement-procedures"></a><span data-ttu-id="cf73d-151">硬體元件更換程序</span><span class="sxs-lookup"><span data-stu-id="cf73d-151">Hardware component replacement procedures</span></span>
<span data-ttu-id="cf73d-152">StoreSimple 8000 系列裝置由主要和/或 EBOD 機箱的數個外掛程式模組所組成。</span><span class="sxs-lookup"><span data-stu-id="cf73d-152">Your StorSimple 8000 series device consists of several plug-in modules in the primary and/or EBOD enclosures.</span></span> <span data-ttu-id="cf73d-153">8100 具有單一主要機箱，而 8600 是具有主要機箱與 EBOD 機箱的雙重機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="cf73d-153">The 8100 has a single primary enclosure, whereas the 8600 is a dual enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

<span data-ttu-id="cf73d-154">下表彙總裝置中的主要硬體元件。</span><span class="sxs-lookup"><span data-stu-id="cf73d-154">The main hardware components in your device are summarized in the following tables.</span></span> <span data-ttu-id="cf73d-155">按一下 [更換程序]  資料行中的連結，即可移到相關聯的教學課程。</span><span class="sxs-lookup"><span data-stu-id="cf73d-155">Click the link in the **Replacement procedure** column to go to the associated tutorial.</span></span>

| <span data-ttu-id="cf73d-156">元件</span><span class="sxs-lookup"><span data-stu-id="cf73d-156">Components</span></span> | <span data-ttu-id="cf73d-157"># Present</span><span class="sxs-lookup"><span data-stu-id="cf73d-157"># Present</span></span> | <span data-ttu-id="cf73d-158">外掛程式模組？</span><span class="sxs-lookup"><span data-stu-id="cf73d-158">Plug-in module?</span></span> | <span data-ttu-id="cf73d-159">更換程序</span><span class="sxs-lookup"><span data-stu-id="cf73d-159">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cf73d-160">底座</span><span class="sxs-lookup"><span data-stu-id="cf73d-160">Chassis</span></span> |<span data-ttu-id="cf73d-161">1</span><span class="sxs-lookup"><span data-stu-id="cf73d-161">1</span></span> |<span data-ttu-id="cf73d-162">否</span><span class="sxs-lookup"><span data-stu-id="cf73d-162">No</span></span> |[<span data-ttu-id="cf73d-163">更換 StorSimple 裝置上的底座</span><span class="sxs-lookup"><span data-stu-id="cf73d-163">Replace the chassis on your StorSimple device</span></span>](storsimple-8000-chassis-replacement.md) |
| <span data-ttu-id="cf73d-164">主要控制器</span><span class="sxs-lookup"><span data-stu-id="cf73d-164">Primary controllers</span></span> |<span data-ttu-id="cf73d-165">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-165">2</span></span> |<span data-ttu-id="cf73d-166">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-166">Yes</span></span> |[<span data-ttu-id="cf73d-167">更換 StorSimple 裝置上的控制器模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-167">Replace a controller module on your StorSimple device</span></span>](storsimple-8000-controller-replacement.md) |
| <span data-ttu-id="cf73d-168">764 瓦電源和冷卻模組 (PCM)</span><span class="sxs-lookup"><span data-stu-id="cf73d-168">764W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="cf73d-169">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-169">2</span></span> |<span data-ttu-id="cf73d-170">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-170">Yes</span></span> |[<span data-ttu-id="cf73d-171">更換 StorSimple 裝置上的電源和冷卻模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-171">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-8000-power-cooling-module-replacement.md) |
| <span data-ttu-id="cf73d-172">備用電池</span><span class="sxs-lookup"><span data-stu-id="cf73d-172">Backup battery</span></span> |<span data-ttu-id="cf73d-173">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-173">2</span></span> |<span data-ttu-id="cf73d-174">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-174">Yes</span></span> |[<span data-ttu-id="cf73d-175">更換 StorSimple 裝置上的備用電池模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-175">Replace the backup battery module on your StorSimple device</span></span>](storsimple-8000-battery-replacement.md) |
| <span data-ttu-id="cf73d-176">磁碟機</span><span class="sxs-lookup"><span data-stu-id="cf73d-176">Disk drives</span></span> |<span data-ttu-id="cf73d-177">12</span><span class="sxs-lookup"><span data-stu-id="cf73d-177">12</span></span> |<span data-ttu-id="cf73d-178">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-178">Yes</span></span> |[<span data-ttu-id="cf73d-179">更換 StorSimple 裝置上的磁碟機</span><span class="sxs-lookup"><span data-stu-id="cf73d-179">Replace a disk drive on your StorSimple device</span></span>](storsimple-8000-disk-drive-replacement.md) |

<span data-ttu-id="cf73d-180">**表 1** 主要機箱中的硬體元件</span><span class="sxs-lookup"><span data-stu-id="cf73d-180">**Table 1** Hardware components in the primary enclosure</span></span>

<span data-ttu-id="cf73d-181">主要機箱和 EBOD 機箱在其 I/O 模組中各有不同。</span><span class="sxs-lookup"><span data-stu-id="cf73d-181">The primary enclosure and the EBOD enclosure differ in their I/O modules.</span></span> <span data-ttu-id="cf73d-182">此外，PCM 有具不同的瓦數。</span><span class="sxs-lookup"><span data-stu-id="cf73d-182">Additionally, the PCMs have different wattage.</span></span> <span data-ttu-id="cf73d-183">主要機箱中的 PCM 為 764 瓦，而 EBOD 機箱中的 PCM 則為 580 瓦。主要機箱中的 PCM 也包含備用電池模組。</span><span class="sxs-lookup"><span data-stu-id="cf73d-183">The PCMs in the primary enclosure are 764 W, whereas those in the EBOD enclosure are 580 W. The PCMs in the primary enclosure also contain a backup battery module.</span></span>

| <span data-ttu-id="cf73d-184">元件</span><span class="sxs-lookup"><span data-stu-id="cf73d-184">Components</span></span> | <span data-ttu-id="cf73d-185"># Present</span><span class="sxs-lookup"><span data-stu-id="cf73d-185"># Present</span></span> | <span data-ttu-id="cf73d-186">外掛程式模組？</span><span class="sxs-lookup"><span data-stu-id="cf73d-186">Plug-in module?</span></span> | <span data-ttu-id="cf73d-187">更換程序</span><span class="sxs-lookup"><span data-stu-id="cf73d-187">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cf73d-188">底座</span><span class="sxs-lookup"><span data-stu-id="cf73d-188">Chassis</span></span> |<span data-ttu-id="cf73d-189">1</span><span class="sxs-lookup"><span data-stu-id="cf73d-189">1</span></span> |<span data-ttu-id="cf73d-190">否</span><span class="sxs-lookup"><span data-stu-id="cf73d-190">No</span></span> |[<span data-ttu-id="cf73d-191">更換 StorSimple 裝置上的底座</span><span class="sxs-lookup"><span data-stu-id="cf73d-191">Replace the chassis on your StorSimple device</span></span>](storsimple-8000-chassis-replacement.md) |
| <span data-ttu-id="cf73d-192">EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="cf73d-192">EBOD controllers</span></span> |<span data-ttu-id="cf73d-193">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-193">2</span></span> |<span data-ttu-id="cf73d-194">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-194">Yes</span></span> |[<span data-ttu-id="cf73d-195">更換 StorSimple 裝置上的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="cf73d-195">Replace an EBOD controller on your StorSimple device</span></span>](storsimple-8000-ebod-controller-replacement.md) |
| <span data-ttu-id="cf73d-196">580 瓦電源和冷卻模組 (PCM)</span><span class="sxs-lookup"><span data-stu-id="cf73d-196">580W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="cf73d-197">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-197">2</span></span> |<span data-ttu-id="cf73d-198">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-198">Yes</span></span> |[<span data-ttu-id="cf73d-199">更換 StorSimple 裝置上的電源和冷卻模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-199">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-8000-power-cooling-module-replacement.md) |
| <span data-ttu-id="cf73d-200">磁碟機</span><span class="sxs-lookup"><span data-stu-id="cf73d-200">Disk drives</span></span> |<span data-ttu-id="cf73d-201">12</span><span class="sxs-lookup"><span data-stu-id="cf73d-201">12</span></span> |<span data-ttu-id="cf73d-202">是</span><span class="sxs-lookup"><span data-stu-id="cf73d-202">Yes</span></span> |[<span data-ttu-id="cf73d-203">更換 StorSimple 裝置上的磁碟機</span><span class="sxs-lookup"><span data-stu-id="cf73d-203">Replace a disk drive on your StorSimple device</span></span>](storsimple-8000-disk-drive-replacement.md) |

<span data-ttu-id="cf73d-204">**表 2** EBOD 機箱中的硬體元件</span><span class="sxs-lookup"><span data-stu-id="cf73d-204">**Table 2** Hardware components in the EBOD enclosure</span></span>

<span data-ttu-id="cf73d-205">裝置上的外掛程式模組會在下列前端和後端圖表中反白顯示。</span><span class="sxs-lookup"><span data-stu-id="cf73d-205">The plug-in modules on the device are highlighted in the following front and rear diagrams.</span></span> <span data-ttu-id="cf73d-206">如果需要更換，您可以使用這些圖表，來判斷各種外掛程式模組的位置。</span><span class="sxs-lookup"><span data-stu-id="cf73d-206">You can use these diagrams to determine the location of the various plug-in modules if a replacement is required.</span></span> <span data-ttu-id="cf73d-207">前端圖表顯示磁碟機，而 EBOD 機箱和主要機箱的後端圖表則顯示外掛程式模組。</span><span class="sxs-lookup"><span data-stu-id="cf73d-207">The front diagram shows the disk drives, and the rear diagrams of the EBOD enclosure and the primary enclosure show the plug-in modules.</span></span>

![具有磁碟機的裝置前擋板](./media/storsimple-hardware-component-replacement/IC741028.png)

<span data-ttu-id="cf73d-209">**圖 1** 裝置正面</span><span class="sxs-lookup"><span data-stu-id="cf73d-209">**Figure 1** Front of the device</span></span>

| <span data-ttu-id="cf73d-210">標籤</span><span class="sxs-lookup"><span data-stu-id="cf73d-210">Label</span></span> | <span data-ttu-id="cf73d-211">說明</span><span class="sxs-lookup"><span data-stu-id="cf73d-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf73d-212">0 - 11</span><span class="sxs-lookup"><span data-stu-id="cf73d-212">0 - 11</span></span> |<span data-ttu-id="cf73d-213">磁碟機 (總共 12 部)</span><span class="sxs-lookup"><span data-stu-id="cf73d-213">Disk drives (total of 12)</span></span> |

<span data-ttu-id="cf73d-214">主要機箱和 EBOD 機箱都具有磁碟機載具模組。</span><span class="sxs-lookup"><span data-stu-id="cf73d-214">Both the primary enclosure and the EBOD enclosure have drive carrier modules.</span></span> <span data-ttu-id="cf73d-215">底座裝載十二部 3.5"磁碟機，依 3 x 4 格式排列。</span><span class="sxs-lookup"><span data-stu-id="cf73d-215">The chassis houses twelve 3.5" disk drives arranged in a 3 by 4 format.</span></span>

![裝置主要機箱模組的後擋板](./media/storsimple-hardware-component-replacement/IC740994.png)

<span data-ttu-id="cf73d-217">**圖 2** 主要機箱背面</span><span class="sxs-lookup"><span data-stu-id="cf73d-217">**Figure 2** Back of the primary enclosure</span></span>

| <span data-ttu-id="cf73d-218">標籤</span><span class="sxs-lookup"><span data-stu-id="cf73d-218">Label</span></span> | <span data-ttu-id="cf73d-219">說明</span><span class="sxs-lookup"><span data-stu-id="cf73d-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf73d-220">1</span><span class="sxs-lookup"><span data-stu-id="cf73d-220">1</span></span> |<span data-ttu-id="cf73d-221">PCM 0</span><span class="sxs-lookup"><span data-stu-id="cf73d-221">PCM 0</span></span> |
| <span data-ttu-id="cf73d-222">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-222">2</span></span> |<span data-ttu-id="cf73d-223">PCM 1</span><span class="sxs-lookup"><span data-stu-id="cf73d-223">PCM 1</span></span> |
| <span data-ttu-id="cf73d-224">3</span><span class="sxs-lookup"><span data-stu-id="cf73d-224">3</span></span> |<span data-ttu-id="cf73d-225">控制器 0</span><span class="sxs-lookup"><span data-stu-id="cf73d-225">Controller 0</span></span> |
| <span data-ttu-id="cf73d-226">4</span><span class="sxs-lookup"><span data-stu-id="cf73d-226">4</span></span> |<span data-ttu-id="cf73d-227">控制器 1</span><span class="sxs-lookup"><span data-stu-id="cf73d-227">Controller 1</span></span> |

![裝置 EBOD 機箱外掛程式模組的後擋板](./media/storsimple-hardware-component-replacement/IC769599.png)

<span data-ttu-id="cf73d-229">**圖 3** EBOD 機箱背面</span><span class="sxs-lookup"><span data-stu-id="cf73d-229">**Figure 3** Back of the EBOD enclosure</span></span>

| <span data-ttu-id="cf73d-230">標籤</span><span class="sxs-lookup"><span data-stu-id="cf73d-230">Label</span></span> | <span data-ttu-id="cf73d-231">說明</span><span class="sxs-lookup"><span data-stu-id="cf73d-231">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cf73d-232">1</span><span class="sxs-lookup"><span data-stu-id="cf73d-232">1</span></span> |<span data-ttu-id="cf73d-233">PCM 0</span><span class="sxs-lookup"><span data-stu-id="cf73d-233">PCM 0</span></span> |
| <span data-ttu-id="cf73d-234">2</span><span class="sxs-lookup"><span data-stu-id="cf73d-234">2</span></span> |<span data-ttu-id="cf73d-235">PCM 1</span><span class="sxs-lookup"><span data-stu-id="cf73d-235">PCM 1</span></span> |
| <span data-ttu-id="cf73d-236">3</span><span class="sxs-lookup"><span data-stu-id="cf73d-236">3</span></span> |<span data-ttu-id="cf73d-237">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="cf73d-237">EBOD Controller 0</span></span> |
| <span data-ttu-id="cf73d-238">4</span><span class="sxs-lookup"><span data-stu-id="cf73d-238">4</span></span> |<span data-ttu-id="cf73d-239">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="cf73d-239">EBOD Controller 1</span></span> |

## <a name="field-replaceable-units"></a><span data-ttu-id="cf73d-240">現場可更換裝置</span><span class="sxs-lookup"><span data-stu-id="cf73d-240">Field replaceable units</span></span>
<span data-ttu-id="cf73d-241">下列現場可更換裝置 (FRU) 可供您的 StorSimple 裝置使用：</span><span class="sxs-lookup"><span data-stu-id="cf73d-241">The following field replaceable units (FRUs) are available for your StorSimple device:</span></span>

* <span data-ttu-id="cf73d-242">底座 (包括整合的操作面板)</span><span class="sxs-lookup"><span data-stu-id="cf73d-242">Chassis (including the integrated operations panel)</span></span>
* <span data-ttu-id="cf73d-243">764 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="cf73d-243">764 W AC PCM</span></span>
* <span data-ttu-id="cf73d-244">580 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="cf73d-244">580 W AC PCM</span></span>
* <span data-ttu-id="cf73d-245">具有磁碟機載具模組的硬碟機</span><span class="sxs-lookup"><span data-stu-id="cf73d-245">Hard disk drive with drive carrier module</span></span>
* <span data-ttu-id="cf73d-246">控制器模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-246">Controller module</span></span>
* <span data-ttu-id="cf73d-247">EBOD 控制器模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-247">EBOD controller module</span></span>
* <span data-ttu-id="cf73d-248">備用電池模組</span><span class="sxs-lookup"><span data-stu-id="cf73d-248">Backup battery module</span></span>
* <span data-ttu-id="cf73d-249">機架掛接滑軌套件</span><span class="sxs-lookup"><span data-stu-id="cf73d-249">Rack mounting rail kit</span></span>

<span data-ttu-id="cf73d-250">請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) ，來訂購任何上述替換單位。</span><span class="sxs-lookup"><span data-stu-id="cf73d-250">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) to order any of these replacement units.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf73d-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf73d-251">Next steps</span></span>
<span data-ttu-id="cf73d-252">請先閱讀所有 [安全資訊](storsimple-safety.md) ，再嘗試更換 StorSimple 硬體元件。</span><span class="sxs-lookup"><span data-stu-id="cf73d-252">Review all [safety information](storsimple-safety.md) before you attempt to replace a StorSimple hardware component.</span></span>

