---
title: "aaaStorSimple 8000 系列硬體元件更換 |Microsoft 文件"
description: "描述如何 toosafely 取代 hello Pcm、 電池、 控制器模組、 EBOD 控制器、 磁碟機和 StorSimple 裝置的底座。"
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
ms.openlocfilehash: 5baca8ff630a1c064cb8bf7e1024b6590f0d6b81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a><span data-ttu-id="08152-103">更換 StorSimple 8000 系列裝置上的硬體元件</span><span class="sxs-lookup"><span data-stu-id="08152-103">Replace a hardware component on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="08152-104">概觀</span><span class="sxs-lookup"><span data-stu-id="08152-104">Overview</span></span>
<span data-ttu-id="08152-105">hello 硬體元件更換教學課程描述您 Microsoft Azure StorSimple 8000 系列裝置和 hello 步驟需要 tooremove hello 硬體元件，並將其取代。</span><span class="sxs-lookup"><span data-stu-id="08152-105">hello hardware component replacement tutorials describe hello hardware components of your Microsoft Azure StorSimple 8000 series device and hello steps necessary tooremove and replace them.</span></span> <span data-ttu-id="08152-106">這篇文章描述 hello 安全性圖示，提供的指標 toohello 詳細的教學課程中，並列出 hello 可取代的元件。</span><span class="sxs-lookup"><span data-stu-id="08152-106">This article describes hello safety icons, provides pointers toohello detailed tutorials, and lists hello components that are replaceable.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08152-107">然後再嘗試 tooremove 或取代任何 StorSimple 元件，請確定您檢閱 hello[安全圖示慣例](#safety-icon-conventions)和其他[安全措施](storsimple-safety.md)。</span><span class="sxs-lookup"><span data-stu-id="08152-107">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>


### <a name="safety-icon-conventions"></a><span data-ttu-id="08152-108">安全性圖示慣例</span><span class="sxs-lookup"><span data-stu-id="08152-108">Safety icon conventions</span></span>
<span data-ttu-id="08152-109">hello 下表說明用於這些教學課程中的 hello 安全性圖示。</span><span class="sxs-lookup"><span data-stu-id="08152-109">hello following table describes hello safety icons used in these tutorials.</span></span> <span data-ttu-id="08152-110">當您瀏覽 hello 步驟 tooremove 並取代裝置元件特別注意 toothese 安全性圖示。</span><span class="sxs-lookup"><span data-stu-id="08152-110">Pay close attention toothese safety icons as you go through hello steps tooremove and replace device components.</span></span>

| <span data-ttu-id="08152-111">圖示</span><span class="sxs-lookup"><span data-stu-id="08152-111">Icon</span></span> | <span data-ttu-id="08152-112">文字</span><span class="sxs-lookup"><span data-stu-id="08152-112">Text</span></span> | <span data-ttu-id="08152-113">其他資訊</span><span class="sxs-lookup"><span data-stu-id="08152-113">Additional information</span></span> |
|:--- |:--- |:--- |
| ![警告圖示](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="08152-115">**危險！**</span><span class="sxs-lookup"><span data-stu-id="08152-115">**DANGER!**</span></span> |<span data-ttu-id="08152-116">指出危險的情況，如果無法避免，將會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="08152-116">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="08152-117">此一指示文字是有限的 toohello 最危險的狀況。</span><span class="sxs-lookup"><span data-stu-id="08152-117">This signal word is limited toohello most extreme situations.</span></span> |
| ![警告圖示](./media/storsimple-hardware-component-replacement/Warning.png) |<span data-ttu-id="08152-119">**警告！**</span><span class="sxs-lookup"><span data-stu-id="08152-119">**WARNING!**</span></span> |<span data-ttu-id="08152-120">指出危險的情況，如果無法避免，可能會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="08152-120">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| ![注意圖示](./media/storsimple-hardware-component-replacement/Caution.png) |<span data-ttu-id="08152-122">**小心！**</span><span class="sxs-lookup"><span data-stu-id="08152-122">**CAUTION!**</span></span> |<span data-ttu-id="08152-123">指出危險的情況，如果無法避免，可能會導致次要或中度的傷害。</span><span class="sxs-lookup"><span data-stu-id="08152-123">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| ![注意事項圖示](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |<span data-ttu-id="08152-125">**注意事項：**</span><span class="sxs-lookup"><span data-stu-id="08152-125">**NOTICE:**</span></span> |<span data-ttu-id="08152-126">表示重要資訊，但與危險無關。</span><span class="sxs-lookup"><span data-stu-id="08152-126">Indicates information considered important, but not hazard-related.</span></span> |
| ![電擊圖示](./media/storsimple-hardware-component-replacement/Electric.png) |<span data-ttu-id="08152-128">**電擊危險**</span><span class="sxs-lookup"><span data-stu-id="08152-128">**Electrical Shock Hazard**</span></span> |<span data-ttu-id="08152-129">表示高電壓。</span><span class="sxs-lookup"><span data-stu-id="08152-129">Indicates high voltage.</span></span> |
| ![超重圖示](./media/storsimple-hardware-component-replacement/Weight.png) |<span data-ttu-id="08152-131">**超重**</span><span class="sxs-lookup"><span data-stu-id="08152-131">**Heavy Weight**</span></span> | |
| ![沒有使用者可自行維修的零件圖示](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |<span data-ttu-id="08152-133">**沒有使用者可自行維修的零件**</span><span class="sxs-lookup"><span data-stu-id="08152-133">**No User Serviceable Parts**</span></span> |<span data-ttu-id="08152-134">除非受過適當訓練，否則請勿觸碰。</span><span class="sxs-lookup"><span data-stu-id="08152-134">Do not access unless properly trained.</span></span> |
| ![閱讀指示圖示](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |<span data-ttu-id="08152-136">**請先閱讀所有指示**</span><span class="sxs-lookup"><span data-stu-id="08152-136">**Read All Instructions First**</span></span> | |
| ![傾倒危險圖示](./media/storsimple-hardware-component-replacement/TipHazard.png) |<span data-ttu-id="08152-138">**傾倒危險**</span><span class="sxs-lookup"><span data-stu-id="08152-138">**Tip Hazard**</span></span> | |

### <a name="before-you-begin"></a><span data-ttu-id="08152-139">開始之前</span><span class="sxs-lookup"><span data-stu-id="08152-139">Before you begin</span></span>
<span data-ttu-id="08152-140">熟悉您在本教學課程中使用的裝置和安全圖示 hello 安全性資訊。</span><span class="sxs-lookup"><span data-stu-id="08152-140">Familiarize yourself with hello safety information about your device and safety icons used in this tutorial.</span></span> <span data-ttu-id="08152-141">跳過[安全地安裝及操作您的 StorSimple 裝置](storsimple-safety.md)如需完整資訊。</span><span class="sxs-lookup"><span data-stu-id="08152-141">Go too[Safely install and operate your StorSimple device](storsimple-safety.md) for complete information.</span></span> <span data-ttu-id="08152-142">要確定 tooreview hello[安全措施](storsimple-safety.md#handling-precautions)之前處理您的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="08152-142">Be sure tooreview hello [Safety precautions](storsimple-safety.md#handling-precautions) before you handle your StorSimple device.</span></span>

<span data-ttu-id="08152-143">您嘗試 tooreplace 元件之前，請考慮下列資訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="08152-143">Before you attempt tooreplace a component, consider hello following information.</span></span>

<span data-ttu-id="08152-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="08152-144">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png) **WARNING!**</span></span>

* <span data-ttu-id="08152-145">處理 StorSimple 裝置的模組和元件時，請使用靜電防護或防靜電墊，讓您自己適當地接地。</span><span class="sxs-lookup"><span data-stu-id="08152-145">Ground yourself properly by using an electrostatic discharge or antistatic mat when handling modules and components of your StorSimple device.</span></span>
* <span data-ttu-id="08152-146">請勿觸及任何電路。</span><span class="sxs-lookup"><span data-stu-id="08152-146">Do not touch any circuitry.</span></span> <span data-ttu-id="08152-147">使用提供的 hello 控點和輔助線時處理可能有裸露電路系統的元件。</span><span class="sxs-lookup"><span data-stu-id="08152-147">Use hello supplied handles and guides while handling components that may have exposed circuitry.</span></span>

<span data-ttu-id="08152-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="08152-148">![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png) ![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png) **NOTICE:**</span></span>

<span data-ttu-id="08152-149">當您取代的模組，**永遠不會留下空槽中 hello hello 機箱的背面**。</span><span class="sxs-lookup"><span data-stu-id="08152-149">When you replace a module, **NEVER leave an empty bay in hello rear of hello enclosure**.</span></span> <span data-ttu-id="08152-150">取得替換模組或空模組移除 hello 問題的零件之前。</span><span class="sxs-lookup"><span data-stu-id="08152-150">Obtain a replacement or blank module before removing hello problem part.</span></span>

## <a name="hardware-component-replacement-procedures"></a><span data-ttu-id="08152-151">硬體元件更換程序</span><span class="sxs-lookup"><span data-stu-id="08152-151">Hardware component replacement procedures</span></span>
<span data-ttu-id="08152-152">您的 StorSimple 8000 系列裝置是由數個外掛模組中主要的 hello 和/或 EBOD 機箱所組成。</span><span class="sxs-lookup"><span data-stu-id="08152-152">Your StorSimple 8000 series device consists of several plug-in modules in hello primary and/or EBOD enclosures.</span></span> <span data-ttu-id="08152-153">hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="08152-153">hello 8100 has a single primary enclosure, whereas hello 8600 is a dual enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

<span data-ttu-id="08152-154">hello 下表中摘要說明您的裝置中的 hello 主要硬體元件。</span><span class="sxs-lookup"><span data-stu-id="08152-154">hello main hardware components in your device are summarized in hello following tables.</span></span> <span data-ttu-id="08152-155">按一下 hello 中的 hello 連結**更換程序**資料行 toogo toohello 相關教學課程。</span><span class="sxs-lookup"><span data-stu-id="08152-155">Click hello link in hello **Replacement procedure** column toogo toohello associated tutorial.</span></span>

| <span data-ttu-id="08152-156">元件</span><span class="sxs-lookup"><span data-stu-id="08152-156">Components</span></span> | <span data-ttu-id="08152-157"># Present</span><span class="sxs-lookup"><span data-stu-id="08152-157"># Present</span></span> | <span data-ttu-id="08152-158">外掛程式模組？</span><span class="sxs-lookup"><span data-stu-id="08152-158">Plug-in module?</span></span> | <span data-ttu-id="08152-159">更換程序</span><span class="sxs-lookup"><span data-stu-id="08152-159">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08152-160">底座</span><span class="sxs-lookup"><span data-stu-id="08152-160">Chassis</span></span> |<span data-ttu-id="08152-161">1</span><span class="sxs-lookup"><span data-stu-id="08152-161">1</span></span> |<span data-ttu-id="08152-162">否</span><span class="sxs-lookup"><span data-stu-id="08152-162">No</span></span> |[<span data-ttu-id="08152-163">取代您的 StorSimple 裝置上的 hello 底座</span><span class="sxs-lookup"><span data-stu-id="08152-163">Replace hello chassis on your StorSimple device</span></span>](storsimple-8000-chassis-replacement.md) |
| <span data-ttu-id="08152-164">主要控制器</span><span class="sxs-lookup"><span data-stu-id="08152-164">Primary controllers</span></span> |<span data-ttu-id="08152-165">2</span><span class="sxs-lookup"><span data-stu-id="08152-165">2</span></span> |<span data-ttu-id="08152-166">是</span><span class="sxs-lookup"><span data-stu-id="08152-166">Yes</span></span> |[<span data-ttu-id="08152-167">更換 StorSimple 裝置上的控制器模組</span><span class="sxs-lookup"><span data-stu-id="08152-167">Replace a controller module on your StorSimple device</span></span>](storsimple-8000-controller-replacement.md) |
| <span data-ttu-id="08152-168">764 瓦電源和冷卻模組 (PCM)</span><span class="sxs-lookup"><span data-stu-id="08152-168">764W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="08152-169">2</span><span class="sxs-lookup"><span data-stu-id="08152-169">2</span></span> |<span data-ttu-id="08152-170">是</span><span class="sxs-lookup"><span data-stu-id="08152-170">Yes</span></span> |[<span data-ttu-id="08152-171">更換 StorSimple 裝置上的電源和冷卻模組</span><span class="sxs-lookup"><span data-stu-id="08152-171">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-8000-power-cooling-module-replacement.md) |
| <span data-ttu-id="08152-172">備用電池</span><span class="sxs-lookup"><span data-stu-id="08152-172">Backup battery</span></span> |<span data-ttu-id="08152-173">2</span><span class="sxs-lookup"><span data-stu-id="08152-173">2</span></span> |<span data-ttu-id="08152-174">是</span><span class="sxs-lookup"><span data-stu-id="08152-174">Yes</span></span> |[<span data-ttu-id="08152-175">取代您的 StorSimple 裝置上的 hello 備用電池模組</span><span class="sxs-lookup"><span data-stu-id="08152-175">Replace hello backup battery module on your StorSimple device</span></span>](storsimple-8000-battery-replacement.md) |
| <span data-ttu-id="08152-176">磁碟機</span><span class="sxs-lookup"><span data-stu-id="08152-176">Disk drives</span></span> |<span data-ttu-id="08152-177">12</span><span class="sxs-lookup"><span data-stu-id="08152-177">12</span></span> |<span data-ttu-id="08152-178">是</span><span class="sxs-lookup"><span data-stu-id="08152-178">Yes</span></span> |[<span data-ttu-id="08152-179">更換 StorSimple 裝置上的磁碟機</span><span class="sxs-lookup"><span data-stu-id="08152-179">Replace a disk drive on your StorSimple device</span></span>](storsimple-8000-disk-drive-replacement.md) |

<span data-ttu-id="08152-180">**表 1** hello 主要機箱中的硬體元件</span><span class="sxs-lookup"><span data-stu-id="08152-180">**Table 1** Hardware components in hello primary enclosure</span></span>

<span data-ttu-id="08152-181">hello 主要機箱和 hello EBOD 機箱的 I/O 模組不同。</span><span class="sxs-lookup"><span data-stu-id="08152-181">hello primary enclosure and hello EBOD enclosure differ in their I/O modules.</span></span> <span data-ttu-id="08152-182">此外，Pcm hello 瓦數不同。</span><span class="sxs-lookup"><span data-stu-id="08152-182">Additionally, hello PCMs have different wattage.</span></span> <span data-ttu-id="08152-183">hello 主要機箱中的 hello Pcm 為 764 W，而在 hello EBOD 機箱是 580 W hello Pcm 中 hello 主要機箱也包含備用電池模組。</span><span class="sxs-lookup"><span data-stu-id="08152-183">hello PCMs in hello primary enclosure are 764 W, whereas those in hello EBOD enclosure are 580 W. hello PCMs in hello primary enclosure also contain a backup battery module.</span></span>

| <span data-ttu-id="08152-184">元件</span><span class="sxs-lookup"><span data-stu-id="08152-184">Components</span></span> | <span data-ttu-id="08152-185"># Present</span><span class="sxs-lookup"><span data-stu-id="08152-185"># Present</span></span> | <span data-ttu-id="08152-186">外掛程式模組？</span><span class="sxs-lookup"><span data-stu-id="08152-186">Plug-in module?</span></span> | <span data-ttu-id="08152-187">更換程序</span><span class="sxs-lookup"><span data-stu-id="08152-187">Replacement procedure</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="08152-188">底座</span><span class="sxs-lookup"><span data-stu-id="08152-188">Chassis</span></span> |<span data-ttu-id="08152-189">1</span><span class="sxs-lookup"><span data-stu-id="08152-189">1</span></span> |<span data-ttu-id="08152-190">否</span><span class="sxs-lookup"><span data-stu-id="08152-190">No</span></span> |[<span data-ttu-id="08152-191">取代您的 StorSimple 裝置上的 hello 底座</span><span class="sxs-lookup"><span data-stu-id="08152-191">Replace hello chassis on your StorSimple device</span></span>](storsimple-8000-chassis-replacement.md) |
| <span data-ttu-id="08152-192">EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="08152-192">EBOD controllers</span></span> |<span data-ttu-id="08152-193">2</span><span class="sxs-lookup"><span data-stu-id="08152-193">2</span></span> |<span data-ttu-id="08152-194">是</span><span class="sxs-lookup"><span data-stu-id="08152-194">Yes</span></span> |[<span data-ttu-id="08152-195">更換 StorSimple 裝置上的 EBOD 控制器</span><span class="sxs-lookup"><span data-stu-id="08152-195">Replace an EBOD controller on your StorSimple device</span></span>](storsimple-8000-ebod-controller-replacement.md) |
| <span data-ttu-id="08152-196">580 瓦電源和冷卻模組 (PCM)</span><span class="sxs-lookup"><span data-stu-id="08152-196">580W Power and Cooling Modules (PCMs)</span></span> |<span data-ttu-id="08152-197">2</span><span class="sxs-lookup"><span data-stu-id="08152-197">2</span></span> |<span data-ttu-id="08152-198">是</span><span class="sxs-lookup"><span data-stu-id="08152-198">Yes</span></span> |[<span data-ttu-id="08152-199">更換 StorSimple 裝置上的電源和冷卻模組</span><span class="sxs-lookup"><span data-stu-id="08152-199">Replace a Power and Cooling Module on your StorSimple device</span></span>](storsimple-8000-power-cooling-module-replacement.md) |
| <span data-ttu-id="08152-200">磁碟機</span><span class="sxs-lookup"><span data-stu-id="08152-200">Disk drives</span></span> |<span data-ttu-id="08152-201">12</span><span class="sxs-lookup"><span data-stu-id="08152-201">12</span></span> |<span data-ttu-id="08152-202">是</span><span class="sxs-lookup"><span data-stu-id="08152-202">Yes</span></span> |[<span data-ttu-id="08152-203">更換 StorSimple 裝置上的磁碟機</span><span class="sxs-lookup"><span data-stu-id="08152-203">Replace a disk drive on your StorSimple device</span></span>](storsimple-8000-disk-drive-replacement.md) |

<span data-ttu-id="08152-204">**表 2** hello EBOD 機箱中的硬體元件</span><span class="sxs-lookup"><span data-stu-id="08152-204">**Table 2** Hardware components in hello EBOD enclosure</span></span>

<span data-ttu-id="08152-205">hello 裝置上的 hello 外掛模組會在 hello 下列正面和背面圖中反白顯示。</span><span class="sxs-lookup"><span data-stu-id="08152-205">hello plug-in modules on hello device are highlighted in hello following front and rear diagrams.</span></span> <span data-ttu-id="08152-206">如果需要更換的話您可以使用指定的 hello 這些圖表 toodetermine hello 位置各種外掛模組。</span><span class="sxs-lookup"><span data-stu-id="08152-206">You can use these diagrams toodetermine hello location of hello various plug-in modules if a replacement is required.</span></span> <span data-ttu-id="08152-207">hello 正面圖顯示 hello 磁碟機，而 hello 背面圖 hello EBOD 機箱與主要機箱 hello 顯示 hello 外掛模組。</span><span class="sxs-lookup"><span data-stu-id="08152-207">hello front diagram shows hello disk drives, and hello rear diagrams of hello EBOD enclosure and hello primary enclosure show hello plug-in modules.</span></span>

![具有磁碟機的裝置前擋板](./media/storsimple-hardware-component-replacement/IC741028.png)

<span data-ttu-id="08152-209">**圖 1** hello 裝置的正面</span><span class="sxs-lookup"><span data-stu-id="08152-209">**Figure 1** Front of hello device</span></span>

| <span data-ttu-id="08152-210">標籤</span><span class="sxs-lookup"><span data-stu-id="08152-210">Label</span></span> | <span data-ttu-id="08152-211">說明</span><span class="sxs-lookup"><span data-stu-id="08152-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08152-212">0 - 11</span><span class="sxs-lookup"><span data-stu-id="08152-212">0 - 11</span></span> |<span data-ttu-id="08152-213">磁碟機 (總共 12 部)</span><span class="sxs-lookup"><span data-stu-id="08152-213">Disk drives (total of 12)</span></span> |

<span data-ttu-id="08152-214">Hello 主要機箱和 hello EBOD 機箱都有磁碟機拖架模組。</span><span class="sxs-lookup"><span data-stu-id="08152-214">Both hello primary enclosure and hello EBOD enclosure have drive carrier modules.</span></span> <span data-ttu-id="08152-215">hello 底座容納 12 個 3.5"磁碟機以 3 x 4 格式排列。</span><span class="sxs-lookup"><span data-stu-id="08152-215">hello chassis houses twelve 3.5" disk drives arranged in a 3 by 4 format.</span></span>

![裝置主要機箱模組的後擋板](./media/storsimple-hardware-component-replacement/IC740994.png)

<span data-ttu-id="08152-217">**圖 2** hello 主要機箱背面</span><span class="sxs-lookup"><span data-stu-id="08152-217">**Figure 2** Back of hello primary enclosure</span></span>

| <span data-ttu-id="08152-218">標籤</span><span class="sxs-lookup"><span data-stu-id="08152-218">Label</span></span> | <span data-ttu-id="08152-219">說明</span><span class="sxs-lookup"><span data-stu-id="08152-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08152-220">1</span><span class="sxs-lookup"><span data-stu-id="08152-220">1</span></span> |<span data-ttu-id="08152-221">PCM 0</span><span class="sxs-lookup"><span data-stu-id="08152-221">PCM 0</span></span> |
| <span data-ttu-id="08152-222">2</span><span class="sxs-lookup"><span data-stu-id="08152-222">2</span></span> |<span data-ttu-id="08152-223">PCM 1</span><span class="sxs-lookup"><span data-stu-id="08152-223">PCM 1</span></span> |
| <span data-ttu-id="08152-224">3</span><span class="sxs-lookup"><span data-stu-id="08152-224">3</span></span> |<span data-ttu-id="08152-225">控制器 0</span><span class="sxs-lookup"><span data-stu-id="08152-225">Controller 0</span></span> |
| <span data-ttu-id="08152-226">4</span><span class="sxs-lookup"><span data-stu-id="08152-226">4</span></span> |<span data-ttu-id="08152-227">控制器 1</span><span class="sxs-lookup"><span data-stu-id="08152-227">Controller 1</span></span> |

![裝置 EBOD 機箱外掛程式模組的後擋板](./media/storsimple-hardware-component-replacement/IC769599.png)

<span data-ttu-id="08152-229">**圖 3** hello EBOD 機箱的背面</span><span class="sxs-lookup"><span data-stu-id="08152-229">**Figure 3** Back of hello EBOD enclosure</span></span>

| <span data-ttu-id="08152-230">標籤</span><span class="sxs-lookup"><span data-stu-id="08152-230">Label</span></span> | <span data-ttu-id="08152-231">說明</span><span class="sxs-lookup"><span data-stu-id="08152-231">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="08152-232">1</span><span class="sxs-lookup"><span data-stu-id="08152-232">1</span></span> |<span data-ttu-id="08152-233">PCM 0</span><span class="sxs-lookup"><span data-stu-id="08152-233">PCM 0</span></span> |
| <span data-ttu-id="08152-234">2</span><span class="sxs-lookup"><span data-stu-id="08152-234">2</span></span> |<span data-ttu-id="08152-235">PCM 1</span><span class="sxs-lookup"><span data-stu-id="08152-235">PCM 1</span></span> |
| <span data-ttu-id="08152-236">3</span><span class="sxs-lookup"><span data-stu-id="08152-236">3</span></span> |<span data-ttu-id="08152-237">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="08152-237">EBOD Controller 0</span></span> |
| <span data-ttu-id="08152-238">4</span><span class="sxs-lookup"><span data-stu-id="08152-238">4</span></span> |<span data-ttu-id="08152-239">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="08152-239">EBOD Controller 1</span></span> |

## <a name="field-replaceable-units"></a><span data-ttu-id="08152-240">現場可更換裝置</span><span class="sxs-lookup"><span data-stu-id="08152-240">Field replaceable units</span></span>
<span data-ttu-id="08152-241">hello 遵循埸可更換裝置 (Fru) 可供您的 StorSimple 裝置：</span><span class="sxs-lookup"><span data-stu-id="08152-241">hello following field replaceable units (FRUs) are available for your StorSimple device:</span></span>

* <span data-ttu-id="08152-242">底座 （包括 hello 整合的操作面板）</span><span class="sxs-lookup"><span data-stu-id="08152-242">Chassis (including hello integrated operations panel)</span></span>
* <span data-ttu-id="08152-243">764 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="08152-243">764 W AC PCM</span></span>
* <span data-ttu-id="08152-244">580 W AC PCM</span><span class="sxs-lookup"><span data-stu-id="08152-244">580 W AC PCM</span></span>
* <span data-ttu-id="08152-245">具有磁碟機載具模組的硬碟機</span><span class="sxs-lookup"><span data-stu-id="08152-245">Hard disk drive with drive carrier module</span></span>
* <span data-ttu-id="08152-246">控制器模組</span><span class="sxs-lookup"><span data-stu-id="08152-246">Controller module</span></span>
* <span data-ttu-id="08152-247">EBOD 控制器模組</span><span class="sxs-lookup"><span data-stu-id="08152-247">EBOD controller module</span></span>
* <span data-ttu-id="08152-248">備用電池模組</span><span class="sxs-lookup"><span data-stu-id="08152-248">Backup battery module</span></span>
* <span data-ttu-id="08152-249">機架掛接滑軌套件</span><span class="sxs-lookup"><span data-stu-id="08152-249">Rack mounting rail kit</span></span>

<span data-ttu-id="08152-250">請[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)tooorder 其中任何更換裝置。</span><span class="sxs-lookup"><span data-stu-id="08152-250">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder any of these replacement units.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08152-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08152-251">Next steps</span></span>
<span data-ttu-id="08152-252">檢閱所有[安全性資訊](storsimple-safety.md)嘗試 tooreplace StorSimple 硬體元件之前。</span><span class="sxs-lookup"><span data-stu-id="08152-252">Review all [safety information](storsimple-safety.md) before you attempt tooreplace a StorSimple hardware component.</span></span>

