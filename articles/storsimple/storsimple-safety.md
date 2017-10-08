---
title: "StorSimple 裝置的 aaaSafety |Microsoft 文件"
description: "描述安全性慣例、 指導方針與考量，並說明 toosafely 安裝及操作您的 StorSimple 裝置的方式。"
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
ms.openlocfilehash: cb5e24582c0391d7b68cb5c74586815af4b58a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="safely-install-and-operate-your-storsimple-device"></a><span data-ttu-id="473f5-103">安全地安裝和操作您的 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="473f5-103">Safely install and operate your StorSimple device</span></span>
<span data-ttu-id="473f5-104">![警告圖示](./media/storsimple-safety/IC740879.png)
 ![閱讀安全性注意事項圖示](./media/storsimple-safety/IC740885.png) **讀取的安全性和健全狀況資訊**</span><span class="sxs-lookup"><span data-stu-id="473f5-104">![Warning Icon](./media/storsimple-safety/IC740879.png)
![Read Safety Notice Icon](./media/storsimple-safety/IC740885.png) **READ SAFETY AND HEALTH INFORMATION**</span></span>

<span data-ttu-id="473f5-105">讀取所有 hello 安全和本文適用於 tooyour Microsoft Azure StorSimple 裝置的健全狀況資訊。</span><span class="sxs-lookup"><span data-stu-id="473f5-105">Read all hello safety and health information in this article that applies tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="473f5-106">保留所有 hello 書面的指南，隨附於您的 StorSimple 裝置，供日後參考。</span><span class="sxs-lookup"><span data-stu-id="473f5-106">Keep all hello printed guides shipped with your StorSimple device for future reference.</span></span> <span data-ttu-id="473f5-107">失敗 toofollow 指示並正確設定、 使用及保護本產品可以提高嚴重傷害或死亡，或損壞 toohello 裝置或裝置 hello 風險。</span><span class="sxs-lookup"><span data-stu-id="473f5-107">Failure toofollow instructions and properly set up, use, and care for this product can increase hello risk of serious injury or death, or damage toohello device or devices.</span></span> <span data-ttu-id="473f5-108">[本指南的可下載版本](http://www.microsoft.com/download/details.aspx?id=44233) 也可供使用。</span><span class="sxs-lookup"><span data-stu-id="473f5-108">A [downloadable version of this guide](http://www.microsoft.com/download/details.aspx?id=44233) is also available.</span></span>

## <a name="safety-icon-conventions"></a><span data-ttu-id="473f5-109">安全性圖示慣例</span><span class="sxs-lookup"><span data-stu-id="473f5-109">Safety icon conventions</span></span>
<span data-ttu-id="473f5-110">以下是您會發現，當您檢閱設定和執行您的 Microsoft Azure StorSimple 裝置時，觀察到的 hello 安全預防措施 toobe hello 圖示。</span><span class="sxs-lookup"><span data-stu-id="473f5-110">Here are hello icons that you will find when you review hello safety precautions toobe observed when setting up and running your Microsoft Azure StorSimple device.</span></span>

| <span data-ttu-id="473f5-111">圖示</span><span class="sxs-lookup"><span data-stu-id="473f5-111">Icon</span></span> | <span data-ttu-id="473f5-112">說明</span><span class="sxs-lookup"><span data-stu-id="473f5-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="473f5-113">![危險圖示](./media/storsimple-safety/IC740879.png) **危險！**</span><span class="sxs-lookup"><span data-stu-id="473f5-113">![Danger Icon](./media/storsimple-safety/IC740879.png) **DANGER!**</span></span> |<span data-ttu-id="473f5-114">指出危險的情況，如果無法避免，將會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="473f5-114">Indicates a hazardous situation that, if not avoided, will result in death or serious injury.</span></span> <span data-ttu-id="473f5-115">此一指示文字是 toobe 有限 toohello 最危險的狀況。</span><span class="sxs-lookup"><span data-stu-id="473f5-115">This signal word is toobe limited toohello most extreme situations.</span></span> |
| <span data-ttu-id="473f5-116">![警告圖示](./media/storsimple-safety/IC740879.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-116">![Warning Icon](./media/storsimple-safety/IC740879.png) **WARNING!**</span></span> |<span data-ttu-id="473f5-117">指出危險的情況，如果無法避免，可能會導致死亡或嚴重傷害。</span><span class="sxs-lookup"><span data-stu-id="473f5-117">Indicates a hazardous situation that, if not avoided, could result in death or serious injury.</span></span> |
| <span data-ttu-id="473f5-118">![警告圖示](./media/storsimple-safety/IC740879.png) **小心！**</span><span class="sxs-lookup"><span data-stu-id="473f5-118">![Warning Icon](./media/storsimple-safety/IC740879.png) **CAUTION!**</span></span> |<span data-ttu-id="473f5-119">指出危險的情況，如果無法避免，可能會導致次要或中度的傷害。</span><span class="sxs-lookup"><span data-stu-id="473f5-119">Indicates a hazardous situation that, if not avoided, could result in minor or moderate injury.</span></span> |
| <span data-ttu-id="473f5-120">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="473f5-120">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span> |<span data-ttu-id="473f5-121">表示重要資訊，但與危險無關。</span><span class="sxs-lookup"><span data-stu-id="473f5-121">Indicates information considered important, but not hazard-related.</span></span> |
| <span data-ttu-id="473f5-122">![電擊圖示](./media/storsimple-safety/IC740882.png) **電擊危險**</span><span class="sxs-lookup"><span data-stu-id="473f5-122">![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **Electrical Shock Hazard**</span></span> |<span data-ttu-id="473f5-123">高電壓</span><span class="sxs-lookup"><span data-stu-id="473f5-123">High voltage</span></span> |
| <span data-ttu-id="473f5-124">![超重圖示](./media/storsimple-safety/IC740883.png) **重量**</span><span class="sxs-lookup"><span data-stu-id="473f5-124">![Heavy Weight Icon](./media/storsimple-safety/IC740883.png) **Heavy Weight**</span></span> | |
| <span data-ttu-id="473f5-125">![沒有使用者可自行維修零件圖示](./media/storsimple-safety/IC740879.png) **沒有使用者可自行維修的零件**</span><span class="sxs-lookup"><span data-stu-id="473f5-125">![No User Serviceable Parts Icon](./media/storsimple-safety/IC740879.png) **No User Serviceable Parts**</span></span> |<span data-ttu-id="473f5-126">除非受過適當訓練，否則請勿觸碰。</span><span class="sxs-lookup"><span data-stu-id="473f5-126">Do not access unless properly trained.</span></span> |
| <span data-ttu-id="473f5-127">![閱讀安全性注意事項圖示](./media/storsimple-safety/IC740885.png)**請先閱讀所有指示**</span><span class="sxs-lookup"><span data-stu-id="473f5-127">![Read Safety Notice Icon](./media/storsimple-safety/IC740885.png)**Read All Instructions First**</span></span> | |
| <span data-ttu-id="473f5-128">![傾倒危險圖示](./media/storsimple-safety/IC740886.png) **傾倒危險**</span><span class="sxs-lookup"><span data-stu-id="473f5-128">![Tip Hazard Icon](./media/storsimple-safety/IC740886.png) **Tip Hazard**</span></span> | |

## <a name="handling-precautions"></a><span data-ttu-id="473f5-129">處理預防措施</span><span class="sxs-lookup"><span data-stu-id="473f5-129">Handling precautions</span></span>
<span data-ttu-id="473f5-130">![警告圖示](./media/storsimple-safety/IC740879.png) ![超重圖示](./media/storsimple-safety/IC740883.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-130">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Heavy Weight Icon](./media/storsimple-safety/IC740883.png) **WARNING!**</span></span> 

<span data-ttu-id="473f5-131">tooreduce hello 造成傷害的風險：</span><span class="sxs-lookup"><span data-stu-id="473f5-131">tooreduce hello risk of injury:</span></span>

* <span data-ttu-id="473f5-132">完全設定的機箱重量向上 too32 公斤 （70 磅）;請勿嘗試 toolift 它自己。</span><span class="sxs-lookup"><span data-stu-id="473f5-132">A fully configured enclosure can weigh up too32 kg (70 lbs); do not try toolift it by yourself.</span></span>
* <span data-ttu-id="473f5-133">之前移動 hello 機箱，務必確定兩個人員是可用 toohandle hello 權數。</span><span class="sxs-lookup"><span data-stu-id="473f5-133">Before moving hello enclosure, always ensure that two people are available toohandle hello weight.</span></span> <span data-ttu-id="473f5-134">請注意，一個人嘗試 toolift 此重量受傷。</span><span class="sxs-lookup"><span data-stu-id="473f5-134">Be aware that one person attempting toolift this weight can sustain injuries.</span></span>
* <span data-ttu-id="473f5-135">不提起 hello 機箱 hello 電源和冷卻模組 (Pcm) 上的 hello 控點位於 hello 背面固定的 hello 單位。</span><span class="sxs-lookup"><span data-stu-id="473f5-135">Do not lift hello enclosure by hello handles on hello Power and Cooling Modules (PCMs) located at hello rear of hello unit.</span></span> <span data-ttu-id="473f5-136">這些不是設計 tootake hello 權數。</span><span class="sxs-lookup"><span data-stu-id="473f5-136">These are not designed tootake hello weight.</span></span>

## <a name="connection-precautions"></a><span data-ttu-id="473f5-137">連接預防措施</span><span class="sxs-lookup"><span data-stu-id="473f5-137">Connection precautions</span></span>
<span data-ttu-id="473f5-138">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-138">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="473f5-139">tooreduce hello 發生傷害、 電擊或死亡的可能性：</span><span class="sxs-lookup"><span data-stu-id="473f5-139">tooreduce hello likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="473f5-140">由多個 AC 來源提供電源時，請中斷所有供應電源以達完全隔離。</span><span class="sxs-lookup"><span data-stu-id="473f5-140">When powered by multiple AC sources, disconnect all supply power for complete isolation.</span></span>
* <span data-ttu-id="473f5-141">在移動它之前，或如果您認為裝置已損壞以任何方式永久拔下 hello 單位。</span><span class="sxs-lookup"><span data-stu-id="473f5-141">Permanently unplug hello unit before you move it or if you think it has become damaged in any way.</span></span>
* <span data-ttu-id="473f5-142">提供安全電子接地連線 toohello 電源供應器線。</span><span class="sxs-lookup"><span data-stu-id="473f5-142">Provide a safe electrical earth connection toohello power supply cords.</span></span> <span data-ttu-id="473f5-143">確認 hello 機箱的 hello 通電之前套用電源符合 hello 國家和當地要求。</span><span class="sxs-lookup"><span data-stu-id="473f5-143">Verify that hello grounding of hello enclosure meets hello national and local requirements before applying power.</span></span>
* <span data-ttu-id="473f5-144">請確定 hello 電源連線一律中斷連線之前 toohello 卸下 PCM 從 hello 機箱。</span><span class="sxs-lookup"><span data-stu-id="473f5-144">Ensure that hello power connection is always disconnected prior toohello removal of a PCM from hello enclosure.</span></span>
* <span data-ttu-id="473f5-145">假設 hello 上 hello 電源線的插頭是主要的 hello 中斷連線的裝置，請確定 hello 插座位於 hello 設備附近並可輕易存取。</span><span class="sxs-lookup"><span data-stu-id="473f5-145">Given that hello plug on hello power supply cord is hello main disconnect device, ensure that hello socket outlets are located near hello equipment and are easily accessible.</span></span>

<span data-ttu-id="473f5-146">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-146">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="473f5-147">tooreduce hello 發生過熱或火災的 hello 電子連線的可能性：</span><span class="sxs-lookup"><span data-stu-id="473f5-147">tooreduce hello likelihood of overheating or fire from hello electrical connections:</span></span>

* <span data-ttu-id="473f5-148">提供的適當電源來源具有電路超載保護 toomeet hello hello 技術規格中詳述的需求。</span><span class="sxs-lookup"><span data-stu-id="473f5-148">Provide a suitable power source with electrical overload protection toomeet hello requirements detailed in hello technical specification.</span></span>
* <span data-ttu-id="473f5-149">請勿使用分叉的電源線 ("Y" 引線)。</span><span class="sxs-lookup"><span data-stu-id="473f5-149">Do not use bifurcated power cords (“Y” leads).</span></span>
* <span data-ttu-id="473f5-150">應移除 toocomply 與適用的安全、 放射性和熱力需求，無封面及所有機槽都必須填入外掛模組或磁碟機空殼。</span><span class="sxs-lookup"><span data-stu-id="473f5-150">toocomply with applicable safety, emission, and thermal requirements, no covers should be removed and all bays must be populated with plug-in modules or drive blanks.</span></span>
* <span data-ttu-id="473f5-151">請 hello 設備用於 hello 製造商所指定的方式。</span><span class="sxs-lookup"><span data-stu-id="473f5-151">Ensure that hello equipment is used in a manner specified by hello manufacturer.</span></span> <span data-ttu-id="473f5-152">如果未指定 hello 製造商的方式使用此設備，可能會減損 hello hello 設備所提供的保護。</span><span class="sxs-lookup"><span data-stu-id="473f5-152">If this equipment is used in a manner not specified by hello manufacturer, hello protection provided by hello equipment may be impaired.</span></span>

<span data-ttu-id="473f5-153">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="473f5-153">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="473f5-154">設備與 tooprevent 產品損毀 hello 正常運作：</span><span class="sxs-lookup"><span data-stu-id="473f5-154">For hello proper operation of your equipment and tooprevent product damage:</span></span>

* <span data-ttu-id="473f5-155">在 hello hello 裝置背面的 hello RJ45 連接埠是只將乙太網路連線。</span><span class="sxs-lookup"><span data-stu-id="473f5-155">hello RJ45 ports at hello back of hello device are for an Ethernet connection only.</span></span> <span data-ttu-id="473f5-156">這些不能連接的 tooa 電信網路。</span><span class="sxs-lookup"><span data-stu-id="473f5-156">These must not be connected tooa telecommunications network.</span></span>
* <span data-ttu-id="473f5-157">是確定 tooinstall hello 裝置可以容納由前至後冷卻設計的機架中。</span><span class="sxs-lookup"><span data-stu-id="473f5-157">Be sure tooinstall hello device in a rack that can accommodate a front-to-back cooling design.</span></span>
* <span data-ttu-id="473f5-158">所有外掛模組和盲屬於 hello 系統機箱。</span><span class="sxs-lookup"><span data-stu-id="473f5-158">All plug-in modules and blank plates are part of hello system enclosure.</span></span> <span data-ttu-id="473f5-159">立即加入替代項目時必須只能將其移除。</span><span class="sxs-lookup"><span data-stu-id="473f5-159">These must only be removed when a replacement can be immediately added.</span></span> <span data-ttu-id="473f5-160">必須執行 hello 系統，不所有模組或空殼的位置。</span><span class="sxs-lookup"><span data-stu-id="473f5-160">hello system must not be run without all modules or blanks in place.</span></span>

## <a name="rack-system-precautions"></a><span data-ttu-id="473f5-161">機架系統預防措施</span><span class="sxs-lookup"><span data-stu-id="473f5-161">Rack system precautions</span></span>
<span data-ttu-id="473f5-162">hello 下列安全需求時，必須考慮掛接在機架封包中的 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="473f5-162">hello following safety requirements must be considered when you mount hello device in a rack cabinet.</span></span>

<span data-ttu-id="473f5-163">![警告圖示](./media/storsimple-safety/IC740879.png) ![傾倒危險圖示](./media/storsimple-safety/IC740886.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-163">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Tip Hazard Icon](./media/storsimple-safety/IC740886.png) **WARNING!**</span></span>

<span data-ttu-id="473f5-164">提示，以透過造成傷害 tooreduce hello 可能性：</span><span class="sxs-lookup"><span data-stu-id="473f5-164">tooreduce hello likelihood of injury from a tip over:</span></span>

* <span data-ttu-id="473f5-165">hello 機架設計應支援 hello 總 hello 安裝機箱重量，而且應具備適當的穩定功能適合 tooprevent hello 機架傾倒或被推倒在安裝或正常使用期間從。</span><span class="sxs-lookup"><span data-stu-id="473f5-165">hello rack design should support hello total weight of hello installed enclosures and should incorporate stabilizing features suitable tooprevent hello rack from tipping or being pushed over during installation or normal use.</span></span>
* <span data-ttu-id="473f5-166">載入機架時, 填滿從 hello 下 hello 機架和 hello 由上而下清空。</span><span class="sxs-lookup"><span data-stu-id="473f5-166">When loading a rack, fill hello rack from hello bottom up and empty from hello top down.</span></span>
* <span data-ttu-id="473f5-167">不滑出 hello 機架在時間 tooavoid hello hello 機架傾倒的危險的多個機箱。</span><span class="sxs-lookup"><span data-stu-id="473f5-167">Do not slide more than one enclosure out of hello rack at a time tooavoid hello danger of hello rack toppling over.</span></span>

<span data-ttu-id="473f5-168">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-168">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="473f5-169">tooreduce hello 發生傷害、 電擊或死亡的可能性：</span><span class="sxs-lookup"><span data-stu-id="473f5-169">tooreduce hello likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="473f5-170">hello 機架應有安全的配電系統。</span><span class="sxs-lookup"><span data-stu-id="473f5-170">hello rack should have a safe electrical distribution system.</span></span> <span data-ttu-id="473f5-171">它必須提供 hello 機箱的電流保護，而且必須未多載所安裝機箱的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="473f5-171">It must provide over-current protection for hello enclosure and must not be overloaded by hello total number of enclosures installed.</span></span> <span data-ttu-id="473f5-172">應該要觀察 hello 名牌上顯示的 hello 電力消耗評等。</span><span class="sxs-lookup"><span data-stu-id="473f5-172">hello electrical power consumption rating shown on hello nameplate should be observed.</span></span>
* <span data-ttu-id="473f5-173">hello 配電系統必須 hello 機架中的每個機箱提供可靠的接地。</span><span class="sxs-lookup"><span data-stu-id="473f5-173">hello electrical distribution system must provide a reliable ground for each enclosure in hello rack.</span></span>
* <span data-ttu-id="473f5-174">hello 設計 hello 配電系統必須將納入考量 hello 總接地外洩目前從所有機箱中的所有電源供應器。</span><span class="sxs-lookup"><span data-stu-id="473f5-174">hello design of hello electrical distribution system must take into consideration hello total ground leakage current from all power supplies in all enclosures.</span></span> <span data-ttu-id="473f5-175">請注意，每個機箱中的每個電源供應器都有最大值 1.0 mA，60 Hz、264 伏特的漏地電流。</span><span class="sxs-lookup"><span data-stu-id="473f5-175">Note that each power supply in each enclosure has a ground leakage current of 1.0 mA maximum at 60 Hz, 264 volts.</span></span> <span data-ttu-id="473f5-176">hello 機架可能必須標示為 「 HIGH LEAKAGE CURRENT。</span><span class="sxs-lookup"><span data-stu-id="473f5-176">hello rack may require labeling with “HIGH LEAKAGE CURRENT.</span></span> <span data-ttu-id="473f5-177">在連接供應電源之前，接地 (接地) 是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="473f5-177">Ground (earth) connection is essential before connecting a supply.”</span></span>
* <span data-ttu-id="473f5-178">hello 機架，hello 機箱設定時，必須符合 UL 60950-1 和 IEC 60950-1/EN 60950-1 的 hello 安全需求。</span><span class="sxs-lookup"><span data-stu-id="473f5-178">hello rack, when configured with hello enclosures, must meet hello safety requirements of UL 60950-1 and IEC 60950-1/EN 60950-1.</span></span>

<span data-ttu-id="473f5-179">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="473f5-179">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="473f5-180">適當的機架系統冷卻 hello:</span><span class="sxs-lookup"><span data-stu-id="473f5-180">For hello proper cooling of your rack system:</span></span>

* <span data-ttu-id="473f5-181">請確定 hello 機架設計列入考量 hello 最大機箱作業周圍溫度攝氏 35 度 （華氏 95 度）。</span><span class="sxs-lookup"><span data-stu-id="473f5-181">Ensure that hello rack design takes into consideration hello maximum enclosure operating ambient temperature of 35 degrees Celsius (95 degrees Fahrenheit).</span></span>
* <span data-ttu-id="473f5-182">hello 系統以低壓、 尾段排氣安裝操作 （背壓建立機架門和障礙物所產生不 tooexceed 5 帕 [0.5 mm 水位計]）。</span><span class="sxs-lookup"><span data-stu-id="473f5-182">hello system is operated with low-pressure, rear-exhaust installation (back pressure created by rack doors and obstacles not tooexceed 5 Pascal [0.5 mm water gauge]).</span></span>

## <a name="power-cooling-module-pcm-precautions"></a><span data-ttu-id="473f5-183">電源冷卻模組 (PCM) 預防措施</span><span class="sxs-lookup"><span data-stu-id="473f5-183">Power Cooling Module (PCM) precautions</span></span>
<span data-ttu-id="473f5-184">hello 裝置是設計的 toooperate 搭配兩個 Pcm。</span><span class="sxs-lookup"><span data-stu-id="473f5-184">hello device is designed toooperate with two PCMs.</span></span> <span data-ttu-id="473f5-185">每個 Pcm hello 有電源供應器和雙軸風扇。</span><span class="sxs-lookup"><span data-stu-id="473f5-185">Each of hello PCMs has a power supply and a dual-axis fan.</span></span> <span data-ttu-id="473f5-186">在嚴重狀況下，hello 系統允許一個電源供應器同時繼續正常運作所發生的失敗。</span><span class="sxs-lookup"><span data-stu-id="473f5-186">During a critical condition, hello system allows for a failure of one power supply while continuing normal operations.</span></span> <span data-ttu-id="473f5-187">兩個 PCM (因此和電源供應器) 必須一律安裝。</span><span class="sxs-lookup"><span data-stu-id="473f5-187">Two PCMs (and hence power supplies) must always be installed.</span></span> <span data-ttu-id="473f5-188">單一 PCM 不會提供備援電源。</span><span class="sxs-lookup"><span data-stu-id="473f5-188">A single PCM does not provide redundant power.</span></span> <span data-ttu-id="473f5-189">因此，即使一個 PCM hello 失敗可能會導致停機時間或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="473f5-189">Therefore, hello failure of even one PCM can result in downtime or possible data loss.</span></span>

<span data-ttu-id="473f5-190">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-190">![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **WARNING!**</span></span>

<span data-ttu-id="473f5-191">tooreduce hello 發生傷害、 電擊或死亡的可能性：</span><span class="sxs-lookup"><span data-stu-id="473f5-191">tooreduce hello likelihood of injury, electrical shock, or death:</span></span>

* <span data-ttu-id="473f5-192">不要移除 hello PCM hello 涵蓋。</span><span class="sxs-lookup"><span data-stu-id="473f5-192">Do not remove hello covers from hello PCM.</span></span> <span data-ttu-id="473f5-193">沒有內部觸電的危險。</span><span class="sxs-lookup"><span data-stu-id="473f5-193">There is a danger of electric shock inside.</span></span> <span data-ttu-id="473f5-194">tooreturn hello PCM 並取得替換品，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="473f5-194">tooreturn hello PCM and obtain a replacement, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

<span data-ttu-id="473f5-195">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="473f5-195">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="473f5-196">設備與 tooprevent 產品損毀 hello 正常運作：</span><span class="sxs-lookup"><span data-stu-id="473f5-196">For hello proper operation of your equipment and tooprevent product damage:</span></span>

* <span data-ttu-id="473f5-197">您必須取代 hello 24 小時內失敗的 PCM。</span><span class="sxs-lookup"><span data-stu-id="473f5-197">You must replace hello failed PCM within 24 hours.</span></span> <span data-ttu-id="473f5-198">卸下 PCM 以便更換之後，必須移除後 10 分鐘內完成 hello 取代。</span><span class="sxs-lookup"><span data-stu-id="473f5-198">After a PCM is removed for replacement, hello replacement must be completed within 10 minutes after removal.</span></span>
* <span data-ttu-id="473f5-199">請勿移除 PCM，除非可以立即安裝替代項目。</span><span class="sxs-lookup"><span data-stu-id="473f5-199">Do not remove a PCM unless a replacement can be installed immediately.</span></span> <span data-ttu-id="473f5-200">hello 機箱不必須沒有備妥所有模組來操作。</span><span class="sxs-lookup"><span data-stu-id="473f5-200">hello enclosure must not be operated without all modules in place.</span></span>

## <a name="electrostatic-discharge-esd-precautions"></a><span data-ttu-id="473f5-201">靜電放電 (ESD) 預防措施</span><span class="sxs-lookup"><span data-stu-id="473f5-201">Electrostatic discharge (ESD) precautions</span></span>
<span data-ttu-id="473f5-202">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="473f5-202">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="473f5-203">觀察下列 ESD 相關預防措施 hello。</span><span class="sxs-lookup"><span data-stu-id="473f5-203">Observe hello following ESD-related precautions.</span></span>

* <span data-ttu-id="473f5-204">請確定您已安裝並檢查適合的抗靜電腕或踝帶。</span><span class="sxs-lookup"><span data-stu-id="473f5-204">Ensure that you have installed and checked a suitable antistatic wrist or ankle strap.</span></span>
* <span data-ttu-id="473f5-205">處理模組和元件時，請觀察所有傳統的 ESD 預防措施。</span><span class="sxs-lookup"><span data-stu-id="473f5-205">Observe all conventional ESD precautions when handling modules and components.</span></span>
* <span data-ttu-id="473f5-206">避免接觸後擋板元件和模組連接器。</span><span class="sxs-lookup"><span data-stu-id="473f5-206">Avoid contact with backplane components and module connectors.</span></span>
* <span data-ttu-id="473f5-207">瑕疵擔保未涵蓋 ESD 損害。</span><span class="sxs-lookup"><span data-stu-id="473f5-207">ESD damage is not covered by warranty.</span></span>

## <a name="battery-disposal-precautions"></a><span data-ttu-id="473f5-208">電池處置預防措施</span><span class="sxs-lookup"><span data-stu-id="473f5-208">Battery disposal precautions</span></span>
<span data-ttu-id="473f5-209">hello 電源供應器在暫時、 短期斷電期間所使用記憶體的特殊電池 tooprotect hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="473f5-209">hello power supply uses a special battery tooprotect hello contents of memory during temporary, short-term power outages.</span></span> <span data-ttu-id="473f5-210">hello 電池的固定於 hello PCM 中。</span><span class="sxs-lookup"><span data-stu-id="473f5-210">hello battery is seated in hello PCM.</span></span> <span data-ttu-id="473f5-211">保留 hello 下列幾點 hello 電池相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="473f5-211">Keep hello following information in mind about hello battery.</span></span>

<span data-ttu-id="473f5-212">![警告圖示](./media/storsimple-safety/IC740879.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="473f5-212">![Warning Icon](./media/storsimple-safety/IC740879.png) **WARNING!**</span></span>

<span data-ttu-id="473f5-213">tooreduce hello shorts、 火災、 爆炸、 起火或死亡的風險：</span><span class="sxs-lookup"><span data-stu-id="473f5-213">tooreduce hello risk of shorts, fire, explosion, injury, or death:</span></span>

* <span data-ttu-id="473f5-214">根據國家/地區規定處置使用過的電池。</span><span class="sxs-lookup"><span data-stu-id="473f5-214">Dispose of used batteries in accordance with national/regional regulations.</span></span>
* <span data-ttu-id="473f5-215">請勿拆解、損毀或加熱至高於攝氏 60 度 (華氏 140 度) 或焚毀。</span><span class="sxs-lookup"><span data-stu-id="473f5-215">Do not disassemble, crush, or heat above 60 degrees Celsius (140 degrees Fahrenheit) or incinerate.</span></span> <span data-ttu-id="473f5-216">取代提供電池 hello PCM 電池。</span><span class="sxs-lookup"><span data-stu-id="473f5-216">Replace hello PCM battery with a supplied battery only.</span></span> <span data-ttu-id="473f5-217">使用另一個電池可能有火災或爆炸的風險。</span><span class="sxs-lookup"><span data-stu-id="473f5-217">Use of another battery may present a risk of fire or explosion.</span></span>
* <span data-ttu-id="473f5-218">如果從 hello 電源供應器卸下電池 hello 使用蓋。</span><span class="sxs-lookup"><span data-stu-id="473f5-218">Use protective end caps on hello batteries if these are removed from hello power supply.</span></span>

<span data-ttu-id="473f5-219">![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**</span><span class="sxs-lookup"><span data-stu-id="473f5-219">![Notice Icon](./media/storsimple-safety/IC740881.png) **NOTICE:**</span></span>

<span data-ttu-id="473f5-220">當運送或 hello 電池的空運，請遵循 hello IATA 鋰電池指南文件位於[http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)</span><span class="sxs-lookup"><span data-stu-id="473f5-220">When shipping or otherwise transporting hello batteries by air, follow hello IATA Lithium Battery Guidance document available at [http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)</span></span>

<span data-ttu-id="473f5-221">您已檢閱這些安全注意事項後，hello 下一個步驟是 toounpack，機架並連接裝置纜線。</span><span class="sxs-lookup"><span data-stu-id="473f5-221">After you have reviewed these safety notices, hello next steps are toounpack, rack and cable your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="473f5-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="473f5-222">Next steps</span></span>
* <span data-ttu-id="473f5-223">8100 裝置跳過[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="473f5-223">For an 8100 device, go too[Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md).</span></span>
* <span data-ttu-id="473f5-224">8600 裝置跳過[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="473f5-224">For an 8600 device, go too[Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>

