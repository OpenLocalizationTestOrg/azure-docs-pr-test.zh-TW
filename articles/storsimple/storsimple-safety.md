---
title: "StorSimple 裝置的安全性 | Microsoft Docs"
description: "描述安全性慣例、方針和考量，並說明如何安全地安裝和操作您的 StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: dae6d535-1ca2-4d2b-b221-6819043aa068
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: a178e8880bcbcada9d66eaacf5ccbdb7c55957cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="safely-install-and-operate-your-storsimple-device"></a><span data-ttu-id="71f8b-103">安全地安裝和操作您的 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="71f8b-103">Safely install and operate your StorSimple device</span></span>
<span data-ttu-id="71f8b-104">![警告圖示](./media/storsimple-safety/IC740879.png)
 ![閱讀安全性注意事項圖示](./media/storsimple-safety/IC740885.png) **讀取的安全性和健全狀況資訊**</span><span class="sxs-lookup"><span data-stu-id="71f8b-104">![Warning Icon](./media/storsimple-safety/IC740879.png)
![Read Safety Notice Icon](./media/storsimple-safety/IC740885.png) **READ SAFETY AND HEALTH INFORMATION**</span></span>

<span data-ttu-id="71f8b-105">請閱讀本文中適用於 Microsoft Azure StorSimple 裝置的所有安全性和健全狀況資訊。</span><span class="sxs-lookup"><span data-stu-id="71f8b-105">Read all the safety and health information in this article that applies to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="71f8b-106">保留隨附於 StorSimple 裝置的所有列印指南供日後參考。</span><span class="sxs-lookup"><span data-stu-id="71f8b-106">Keep all the printed guides shipped with your StorSimple device for future reference.</span></span> <span data-ttu-id="71f8b-107">無法遵循下列指示並適當地設定、使用和照顧這項產品可能會提高嚴重傷害或人員死亡的風險，或造成裝置的損毀。</span><span class="sxs-lookup"><span data-stu-id="71f8b-107">Failure to follow instructions and properly set up, use, and care for this product can increase the risk of serious injury or death, or damage to the device or devices.</span></span> <span data-ttu-id="71f8b-108">[本指南的可下載版本](http://www.microsoft.com/download/details.aspx?id=44233) 也可供使用。</span><span class="sxs-lookup"><span data-stu-id="71f8b-108">A [downloadable version of this guide](http://www.microsoft.com/download/details.aspx?id=44233) is also available.</span></span>

## <a name="safety-icon-conventions"></a><span data-ttu-id="71f8b-109">安全性圖示慣例</span><span class="sxs-lookup"><span data-stu-id="71f8b-109">Safety icon conventions</span></span>
<span data-ttu-id="71f8b-110">以下是您在檢閱安全性預防措施時會發現的圖示，這些措施可在設定與執行 Microsoft Azure StorSimple 裝置時觀查到。</span><span class="sxs-lookup"><span data-stu-id="71f8b-110">Here are the icons that you will find when you review the safety precautions to be observed when setting up and running your Microsoft Azure StorSimple device.</span></span>

| <span data-ttu-id="71f8b-111">圖示</span><span class="sxs-lookup"><span data-stu-id="71f8b-111">Icon</span></span> | <span data-ttu-id="71f8b-112">說明</span><span class="sxs-lookup"><span data-stu-id="71f8b-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f8b-113">![危險圖示](./media/storsimple-safety/IC740879.png) **危險！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-113">![Danger Icon](./media/storsimple-safety/IC740879.png) **DANGER!**</span></span> |<span data-ttu-id="71f8b-114">指出危險的情況，如果無法避免，將會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="71f8b-114">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="71f8b-115">此訊號文字僅限用於最極端的情況。</span><span class="sxs-lookup"><span data-stu-id="71f8b-115">This signal word is to be limited to the most extreme situations.</span></span> |
| <span data-ttu-id="71f8b-116">![警告圖示](./media/storsimple-safety/IC740879.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-116">![Warning Icon](./media/storsimple-safety/IC740879.png) **WARNING!**</span></span> |<span data-ttu-id="71f8b-117">指出危險的情況，如果無法避免，可能會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="71f8b-117">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| <span data-ttu-id="71f8b-118">![警告圖示](./media/storsimple-safety/IC740879.png) **小心！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-118">![Warning Icon](./media/storsimple-safety/IC740879.png) **CAUTION!**</span></span> |<span data-ttu-id="71f8b-119">指出危險的情況，如果無法避免，可能會導致次要或中度的傷害。</span><span class="sxs-lookup"><span data-stu-id="71f8b-119">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| <span data-ttu-id="71f8b-120">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="71f8b-120">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span> |<span data-ttu-id="71f8b-121">表示重要資訊，但與危險無關。</span><span class="sxs-lookup"><span data-stu-id="71f8b-121">Indicates information considered important, but not hazard-related.</span></span> |
| <span data-ttu-id="71f8b-122">![電擊圖示](./media/storsimple-safety/IC740882.png) **電擊危險**</span><span class="sxs-lookup"><span data-stu-id="71f8b-122">![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **Electrical Shock Hazard**</span></span> |<span data-ttu-id="71f8b-123">高電壓</span><span class="sxs-lookup"><span data-stu-id="71f8b-123">High voltage</span></span> |
| <span data-ttu-id="71f8b-124">![超重圖示](./media/storsimple-safety/IC740883.png) **重量**</span><span class="sxs-lookup"><span data-stu-id="71f8b-124">![Heavy Weight Icon](./media/storsimple-safety/IC740883.png) **Heavy Weight**</span></span> | |
| <span data-ttu-id="71f8b-125">![沒有使用者可自行維修零件圖示](./media/storsimple-safety/IC740879.png) **沒有使用者可自行維修的零件**</span><span class="sxs-lookup"><span data-stu-id="71f8b-125">![No User Serviceable Parts Icon](./media/storsimple-safety/IC740879.png) **No User Serviceable Parts**</span></span> |<span data-ttu-id="71f8b-126">除非受過適當訓練，否則請勿觸碰。</span><span class="sxs-lookup"><span data-stu-id="71f8b-126">Do not access unless properly trained.</span></span> |
| <span data-ttu-id="71f8b-127">![閱讀安全性注意事項圖示](./media/storsimple-safety/IC740885.png)**請先閱讀所有指示**</span><span class="sxs-lookup"><span data-stu-id="71f8b-127">![Read Safety Notice Icon](./media/storsimple-safety/IC740885.png)**Read All Instructions First**</span></span> | |
| <span data-ttu-id="71f8b-128">![傾倒危險圖示](./media/storsimple-safety/IC740886.png) **傾倒危險**</span><span class="sxs-lookup"><span data-stu-id="71f8b-128">![Tip Hazard Icon](./media/storsimple-safety/IC740886.png) **Tip Hazard**</span></span> | |

## <a name="handling-precautions"></a><span data-ttu-id="71f8b-129">處理預防措施</span><span class="sxs-lookup"><span data-stu-id="71f8b-129">Handling precautions</span></span>
<span data-ttu-id="71f8b-130">![警告圖示](./media/storsimple-safety/IC740879.png) ![超重圖示](./media/storsimple-safety/IC740883.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-130">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Heavy Weight Icon](./media/storsimple-safety/IC740883.png) **WARNING!**</span></span> 

<span data-ttu-id="71f8b-131">減少受傷的風險：</span><span class="sxs-lookup"><span data-stu-id="71f8b-131">To reduce the risk of injury:</span></span>

* <span data-ttu-id="71f8b-132">完整設定的機箱重達 32 公斤 (70 磅)；請勿嘗試自己將其抬起。</span><span class="sxs-lookup"><span data-stu-id="71f8b-132">A fully configured enclosure can weigh up to 32 kg (70 lbs); do not try to lift it by yourself.</span></span>
* <span data-ttu-id="71f8b-133">移動機箱之前，請務必確定由兩人承受重量。</span><span class="sxs-lookup"><span data-stu-id="71f8b-133">Before moving the enclosure, always ensure that two people are available to handle the weight.</span></span> <span data-ttu-id="71f8b-134">請注意，一個人嘗試抬起這個重量可能造成受傷。</span><span class="sxs-lookup"><span data-stu-id="71f8b-134">Be aware that one person attempting to lift this weight can sustain injuries.</span></span>
* <span data-ttu-id="71f8b-135">請勿利用單元後方電源和冷卻模組 (PCM) 上的把手抬起機箱。</span><span class="sxs-lookup"><span data-stu-id="71f8b-135">Do not lift the enclosure by the handles on the Power and Cooling Modules (PCMs) located at the rear of the unit.</span></span> <span data-ttu-id="71f8b-136">這些把手不是設計來承受重量的。</span><span class="sxs-lookup"><span data-stu-id="71f8b-136">These are not designed to take the weight.</span></span>

## <a name="connection-precautions"></a><span data-ttu-id="71f8b-137">連接預防措施</span><span class="sxs-lookup"><span data-stu-id="71f8b-137">Connection precautions</span></span>
<span data-ttu-id="71f8b-138">![警告圖示](./media/storsimple-safety/IC740879.png) ![電擊圖示](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-138">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="71f8b-139">減少傷害、電擊或死亡的可能性：</span><span class="sxs-lookup"><span data-stu-id="71f8b-139">To reduce the likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="71f8b-140">由多個 AC 來源提供電源時，請中斷所有供應電源以達完全隔離。</span><span class="sxs-lookup"><span data-stu-id="71f8b-140">When powered by multiple AC sources, disconnect all supply power for complete isolation.</span></span>
* <span data-ttu-id="71f8b-141">在您移動單元，或者認為單元受到任何損毀時，請一律拔除電源。</span><span class="sxs-lookup"><span data-stu-id="71f8b-141">Permanently unplug the unit before you move it or if you think it has become damaged in any way.</span></span>
* <span data-ttu-id="71f8b-142">提供電源供應線安全的接地線。</span><span class="sxs-lookup"><span data-stu-id="71f8b-142">Provide a safe electrical earth connection to the power supply cords.</span></span> <span data-ttu-id="71f8b-143">請確認機箱接地符合國家和當地需求，然後再供應電源。</span><span class="sxs-lookup"><span data-stu-id="71f8b-143">Verify that the grounding of the enclosure meets the national and local requirements before applying power.</span></span>
* <span data-ttu-id="71f8b-144">從機箱移除 PCM 之前請務必中斷電源連接。</span><span class="sxs-lookup"><span data-stu-id="71f8b-144">Ensure that the power connection is always disconnected prior to the removal of a PCM from the enclosure.</span></span>
* <span data-ttu-id="71f8b-145">假設電源供應線上的插頭是主要的中斷裝置，請確保插座位於設備附近且可輕鬆觸及。</span><span class="sxs-lookup"><span data-stu-id="71f8b-145">Given that the plug on the power supply cord is the main disconnect device, ensure that the socket outlets are located near the equipment and are easily accessible.</span></span>

<span data-ttu-id="71f8b-146">![警告圖示](./media/storsimple-safety/IC740879.png) ![電擊圖示](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-146">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="71f8b-147">降低電力連接過熱或火災的可能性：</span><span class="sxs-lookup"><span data-stu-id="71f8b-147">To reduce the likelihood of overheating or fire from the electrical connections:</span></span>

* <span data-ttu-id="71f8b-148">提供適當的電源及電力多載保護，以符合技術規格中詳細列出的需求。</span><span class="sxs-lookup"><span data-stu-id="71f8b-148">Provide a suitable power source with electrical overload protection to meet the requirements detailed in the technical specification.</span></span>
* <span data-ttu-id="71f8b-149">請勿使用分叉的電源線 ("Y" 引線)。</span><span class="sxs-lookup"><span data-stu-id="71f8b-149">Do not use bifurcated power cords (“Y” leads).</span></span>
* <span data-ttu-id="71f8b-150">若要符合適用的安全性、放射性與熱需求，您不能移除任何封蓋且所有機架必須填入外掛程式模組或磁碟機空白。</span><span class="sxs-lookup"><span data-stu-id="71f8b-150">To comply with applicable safety, emission, and thermal requirements, no covers should be removed and all bays must be populated with plug-in modules or drive blanks.</span></span>
* <span data-ttu-id="71f8b-151">請確定以製造商所指定的方式使用設備。</span><span class="sxs-lookup"><span data-stu-id="71f8b-151">Ensure that the equipment is used in a manner specified by the manufacturer.</span></span> <span data-ttu-id="71f8b-152">如果未以製造商所指定的方式使用設備，設備所提供的保護可能會減損。</span><span class="sxs-lookup"><span data-stu-id="71f8b-152">If this equipment is used in a manner not specified by the manufacturer, the protection provided by the equipment may be impaired.</span></span>

<span data-ttu-id="71f8b-153">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="71f8b-153">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="71f8b-154">讓您的設備正確作業並避免產品損害：</span><span class="sxs-lookup"><span data-stu-id="71f8b-154">For the proper operation of your equipment and to prevent product damage:</span></span>

* <span data-ttu-id="71f8b-155">在裝置背面的 RJ45 連接埠僅適用於乙太網路連線。</span><span class="sxs-lookup"><span data-stu-id="71f8b-155">The RJ45 ports at the back of the device are for an Ethernet connection only.</span></span> <span data-ttu-id="71f8b-156">這些不必連接到電信網路。</span><span class="sxs-lookup"><span data-stu-id="71f8b-156">These must not be connected to a telecommunications network.</span></span>
* <span data-ttu-id="71f8b-157">請務必在可容納前後冷卻設計的機架上安裝該裝置。</span><span class="sxs-lookup"><span data-stu-id="71f8b-157">Be sure to install the device in a rack that can accommodate a front-to-back cooling design.</span></span>
* <span data-ttu-id="71f8b-158">所有外掛程式模組和空白面板都是系統機箱的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f8b-158">All plug-in modules and blank plates are part of the system enclosure.</span></span> <span data-ttu-id="71f8b-159">立即加入替代項目時必須只能將其移除。</span><span class="sxs-lookup"><span data-stu-id="71f8b-159">These must only be removed when a replacement can be immediately added.</span></span> <span data-ttu-id="71f8b-160">系統不能在所有模組或空白都備妥之前執行。</span><span class="sxs-lookup"><span data-stu-id="71f8b-160">The system must not be run without all modules or blanks in place.</span></span>

## <a name="rack-system-precautions"></a><span data-ttu-id="71f8b-161">機架系統預防措施</span><span class="sxs-lookup"><span data-stu-id="71f8b-161">Rack system precautions</span></span>
<span data-ttu-id="71f8b-162">在機櫃中掛接裝置時，必須考量下列安全性需求。</span><span class="sxs-lookup"><span data-stu-id="71f8b-162">The following safety requirements must be considered when you mount the device in a rack cabinet.</span></span>

<span data-ttu-id="71f8b-163">![警告圖示](./media/storsimple-safety/IC740879.png) ![傾倒危險圖示](./media/storsimple-safety/IC740886.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-163">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Tip Hazard Icon](./media/storsimple-safety/IC740886.png) **WARNING!**</span></span>

<span data-ttu-id="71f8b-164">減少因為傾倒而受傷的可能性：</span><span class="sxs-lookup"><span data-stu-id="71f8b-164">To reduce the likelihood of injury from a tip over:</span></span>

* <span data-ttu-id="71f8b-165">機架設計應該支援已安裝機箱的總重量，而且應該納入穩定功能，適用於防止機架在安裝或正常使用期間傾倒或推倒。</span><span class="sxs-lookup"><span data-stu-id="71f8b-165">The rack design should support the total weight of the installed enclosures and should incorporate stabilizing features suitable to prevent the rack from tipping or being pushed over during installation or normal use.</span></span>
* <span data-ttu-id="71f8b-166">載入時機架，從下到上填滿機架並從上到下清空。</span><span class="sxs-lookup"><span data-stu-id="71f8b-166">When loading a rack, fill the rack from the bottom up and empty from the top down.</span></span>
* <span data-ttu-id="71f8b-167">不要一次從機架滑動超過一個機箱，以避免機架倒塌的危險。</span><span class="sxs-lookup"><span data-stu-id="71f8b-167">Do not slide more than one enclosure out of the rack at a time to avoid the danger of the rack toppling over.</span></span>

<span data-ttu-id="71f8b-168">![警告圖示](./media/storsimple-safety/IC740879.png) ![電擊圖示](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-168">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="71f8b-169">減少傷害、電擊或死亡的可能性：</span><span class="sxs-lookup"><span data-stu-id="71f8b-169">To reduce the likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="71f8b-170">機架應該有一個安全的電子散發系統。</span><span class="sxs-lookup"><span data-stu-id="71f8b-170">The rack should have a safe electrical distribution system.</span></span> <span data-ttu-id="71f8b-171">它必須提供機箱的過電流保護，而且安裝的機箱總數不能超載。</span><span class="sxs-lookup"><span data-stu-id="71f8b-171">It must provide over-current protection for the enclosure and must not be overloaded by the total number of enclosures installed.</span></span> <span data-ttu-id="71f8b-172">應該觀察顯示在名牌上的電力消耗評等。</span><span class="sxs-lookup"><span data-stu-id="71f8b-172">The electrical power consumption rating shown on the nameplate should be observed.</span></span>
* <span data-ttu-id="71f8b-173">電力發散系統必須提供可靠的地面給機架中的每個機箱。</span><span class="sxs-lookup"><span data-stu-id="71f8b-173">The electrical distribution system must provide a reliable ground for each enclosure in the rack.</span></span>
* <span data-ttu-id="71f8b-174">電力發散系統的設計必須考量所有機箱中所有電源供應器的總漏地電流。</span><span class="sxs-lookup"><span data-stu-id="71f8b-174">The design of the electrical distribution system must take into consideration the total ground leakage current from all power supplies in all enclosures.</span></span> <span data-ttu-id="71f8b-175">請注意，每個機箱中的每個電源供應器都有最大值 1.0 mA，60 Hz、264 伏特的漏地電流。</span><span class="sxs-lookup"><span data-stu-id="71f8b-175">Note that each power supply in each enclosure has a ground leakage current of 1.0 mA maximum at 60 Hz, 264 volts.</span></span> <span data-ttu-id="71f8b-176">機架可能需要加上下列標籤「高漏地電流。</span><span class="sxs-lookup"><span data-stu-id="71f8b-176">The rack may require labeling with “HIGH LEAKAGE CURRENT.</span></span> <span data-ttu-id="71f8b-177">在連接供應電源之前，接地 (接地) 是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="71f8b-177">Ground (earth) connection is essential before connecting a supply.”</span></span>
* <span data-ttu-id="71f8b-178">利用機箱設定機架時，機架上必須符合 UL 60950-1 和 IEC 60950-1/EN 60950-1 的安全性需求。</span><span class="sxs-lookup"><span data-stu-id="71f8b-178">The rack, when configured with the enclosures, must meet the safety requirements of UL 60950-1 and IEC 60950-1/EN 60950-1.</span></span>

<span data-ttu-id="71f8b-179">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="71f8b-179">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="71f8b-180">關於機架系統的適當冷卻：</span><span class="sxs-lookup"><span data-stu-id="71f8b-180">For the proper cooling of your rack system:</span></span>

* <span data-ttu-id="71f8b-181">請確定機架設計考量到機箱作業周圍溫度最大值為攝氏 35 度 (華氏 95 度)。</span><span class="sxs-lookup"><span data-stu-id="71f8b-181">Ensure that the rack design takes into consideration the maximum enclosure operating ambient temperature of 35 degrees Celsius (95 degrees Fahrenheit).</span></span>
* <span data-ttu-id="71f8b-182">系統在低壓、後方排氣安裝的條件下運作 (機架門和障礙建立的背部壓力不能超過 5 Pascal [0.5 mm-1.0 水位表])。</span><span class="sxs-lookup"><span data-stu-id="71f8b-182">The system is operated with low-pressure, rear-exhaust installation (back pressure created by rack doors and obstacles not to exceed 5 Pascal [0.5 mm water gauge]).</span></span>

## <a name="power-cooling-module-pcm-precautions"></a><span data-ttu-id="71f8b-183">電源冷卻模組 (PCM) 預防措施</span><span class="sxs-lookup"><span data-stu-id="71f8b-183">Power Cooling Module (PCM) precautions</span></span>
<span data-ttu-id="71f8b-184">裝置設計為利用兩個 PCM 運作。</span><span class="sxs-lookup"><span data-stu-id="71f8b-184">The device is designed to operate with two PCMs.</span></span> <span data-ttu-id="71f8b-185">每個 PCM 都具有電源供應器和雙軸風扇。</span><span class="sxs-lookup"><span data-stu-id="71f8b-185">Each of the PCMs has a power supply and a dual-axis fan.</span></span> <span data-ttu-id="71f8b-186">在嚴苛條件期間，系統會允許其中一個電源供應器失敗，同時繼續正常作業。</span><span class="sxs-lookup"><span data-stu-id="71f8b-186">During a critical condition, the system allows for a failure of one power supply while continuing normal operations.</span></span> <span data-ttu-id="71f8b-187">兩個 PCM (因此和電源供應器) 必須一律安裝。</span><span class="sxs-lookup"><span data-stu-id="71f8b-187">Two PCMs (and hence power supplies) must always be installed.</span></span> <span data-ttu-id="71f8b-188">單一 PCM 不會提供備援電源。</span><span class="sxs-lookup"><span data-stu-id="71f8b-188">A single PCM does not provide redundant power.</span></span> <span data-ttu-id="71f8b-189">因此，即使一個 PCM 失敗也可能會導致停機或可能會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="71f8b-189">Therefore, the failure of even one PCM can result in downtime or possible data loss.</span></span>

<span data-ttu-id="71f8b-190">![警告圖示](./media/storsimple-safety/IC740879.png) ![電擊圖示](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-190">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="71f8b-191">減少傷害、電擊或死亡的可能性：</span><span class="sxs-lookup"><span data-stu-id="71f8b-191">To reduce the likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="71f8b-192">請勿從 PCM 移除封蓋。</span><span class="sxs-lookup"><span data-stu-id="71f8b-192">Do not remove the covers from the PCM.</span></span> <span data-ttu-id="71f8b-193">沒有內部觸電的危險。</span><span class="sxs-lookup"><span data-stu-id="71f8b-193">There is a danger of electric shock inside.</span></span> <span data-ttu-id="71f8b-194">若要傳回 PCM 並取得替代項目，請 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="71f8b-194">To return the PCM and obtain a replacement, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

<span data-ttu-id="71f8b-195">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="71f8b-195">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="71f8b-196">讓您的設備正確作業並避免產品損害：</span><span class="sxs-lookup"><span data-stu-id="71f8b-196">For the proper operation of your equipment and to prevent product damage:</span></span>

* <span data-ttu-id="71f8b-197">您必須在 24 小時內取代失敗的 PCM。</span><span class="sxs-lookup"><span data-stu-id="71f8b-197">You must replace the failed PCM within 24 hours.</span></span> <span data-ttu-id="71f8b-198">移除 PCM 以進行取代之後，必須在移除後 10 分鐘內完成取代。</span><span class="sxs-lookup"><span data-stu-id="71f8b-198">After a PCM is removed for replacement, the replacement must be completed within 10 minutes after removal.</span></span>
* <span data-ttu-id="71f8b-199">請勿移除 PCM，除非可以立即安裝替代項目。</span><span class="sxs-lookup"><span data-stu-id="71f8b-199">Do not remove a PCM unless a replacement can be installed immediately.</span></span> <span data-ttu-id="71f8b-200">機箱不得在所有模組尚未備妥之前運作。</span><span class="sxs-lookup"><span data-stu-id="71f8b-200">The enclosure must not be operated without all modules in place.</span></span>

## <a name="electrostatic-discharge-esd-precautions"></a><span data-ttu-id="71f8b-201">靜電放電 (ESD) 預防措施</span><span class="sxs-lookup"><span data-stu-id="71f8b-201">Electrostatic discharge (ESD) precautions</span></span>
<span data-ttu-id="71f8b-202">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="71f8b-202">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="71f8b-203">請遵循下列 ESD 相關的預防措施。</span><span class="sxs-lookup"><span data-stu-id="71f8b-203">Observe the following ESD-related precautions.</span></span>

* <span data-ttu-id="71f8b-204">請確定您已安裝並檢查適合的抗靜電腕或踝帶。</span><span class="sxs-lookup"><span data-stu-id="71f8b-204">Ensure that you have installed and checked a suitable antistatic wrist or ankle strap.</span></span>
* <span data-ttu-id="71f8b-205">處理模組和元件時，請觀察所有傳統的 ESD 預防措施。</span><span class="sxs-lookup"><span data-stu-id="71f8b-205">Observe all conventional ESD precautions when handling modules and components.</span></span>
* <span data-ttu-id="71f8b-206">避免接觸後擋板元件和模組連接器。</span><span class="sxs-lookup"><span data-stu-id="71f8b-206">Avoid contact with backplane components and module connectors.</span></span>
* <span data-ttu-id="71f8b-207">瑕疵擔保未涵蓋 ESD 損害。</span><span class="sxs-lookup"><span data-stu-id="71f8b-207">ESD damage is not covered by warranty.</span></span>

## <a name="battery-disposal-precautions"></a><span data-ttu-id="71f8b-208">電池處置預防措施</span><span class="sxs-lookup"><span data-stu-id="71f8b-208">Battery disposal precautions</span></span>
<span data-ttu-id="71f8b-209">電源供應器會使用特殊的電池，以在暫時的短期電源中斷期間保護記憶體的內容。</span><span class="sxs-lookup"><span data-stu-id="71f8b-209">The power supply uses a special battery to protect the contents of memory during temporary, short-term power outages.</span></span> <span data-ttu-id="71f8b-210">電池置於 PCM 中。</span><span class="sxs-lookup"><span data-stu-id="71f8b-210">The battery is seated in the PCM.</span></span> <span data-ttu-id="71f8b-211">記住下列電池相關資訊。</span><span class="sxs-lookup"><span data-stu-id="71f8b-211">Keep the following information in mind about the battery.</span></span>

<span data-ttu-id="71f8b-212">![警告圖示](./media/storsimple-safety/IC740879.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="71f8b-212">![Warning Icon](./media/storsimple-safety/IC740879.png) **WARNING!**</span></span>

<span data-ttu-id="71f8b-213">減少短路、火災、爆炸、傷害或死亡的風險：</span><span class="sxs-lookup"><span data-stu-id="71f8b-213">To reduce the risk of shorts, fire, explosion, injury, or death:</span></span>

* <span data-ttu-id="71f8b-214">根據國家/地區規定處置使用過的電池。</span><span class="sxs-lookup"><span data-stu-id="71f8b-214">Dispose of used batteries in accordance with national/regional regulations.</span></span>
* <span data-ttu-id="71f8b-215">請勿拆解、損毀或加熱至高於攝氏 60 度 (華氏 140 度) 或焚毀。</span><span class="sxs-lookup"><span data-stu-id="71f8b-215">Do not disassemble, crush, or heat above 60 degrees Celsius (140 degrees Fahrenheit) or incinerate.</span></span> <span data-ttu-id="71f8b-216">只能以提供的電池取代 PCM 電池。</span><span class="sxs-lookup"><span data-stu-id="71f8b-216">Replace the PCM battery with a supplied battery only.</span></span> <span data-ttu-id="71f8b-217">使用另一個電池可能有火災或爆炸的風險。</span><span class="sxs-lookup"><span data-stu-id="71f8b-217">Use of another battery may present a risk of fire or explosion.</span></span>
* <span data-ttu-id="71f8b-218">如果從電源供應器移除電池，請使用電池上的保護端帽。</span><span class="sxs-lookup"><span data-stu-id="71f8b-218">Use protective end caps on the batteries if these are removed from the power supply.</span></span>

<span data-ttu-id="71f8b-219">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="71f8b-219">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="71f8b-220">以空運傳送或傳輸電池時，請遵循 [http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)</span><span class="sxs-lookup"><span data-stu-id="71f8b-220">When shipping or otherwise transporting the batteries by air, follow the IATA Lithium Battery Guidance document available at [http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)</span></span>

<span data-ttu-id="71f8b-221">在您檢閱這些安全性注意事項之後，接下來的步驟是為裝置解除封裝、安裝機架和纜線。</span><span class="sxs-lookup"><span data-stu-id="71f8b-221">After you have reviewed these safety notices, the next steps are to unpack, rack and cable your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71f8b-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71f8b-222">Next steps</span></span>
* <span data-ttu-id="71f8b-223">針對 8100 裝置，請至 [安裝您的 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="71f8b-223">For an 8100 device, go to [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md).</span></span>
* <span data-ttu-id="71f8b-224">針對 8600 裝置，請至 [安裝您的 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="71f8b-224">For an 8600 device, go to [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>

