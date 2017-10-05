---
title: "開啟或關閉 StorSimple 8000 系列裝置 | Microsoft Docs"
description: "說明如何開啟新的 StorSimple 裝置、開啟曾關閉或失去電源的裝置，以及關閉執行中的裝置。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0577c837e0c47ba37a4f586603b0f5b951f1b549
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a><span data-ttu-id="00cdb-103">開啟或關閉 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-103">Turn on or turn off your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="00cdb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="00cdb-104">Overview</span></span>
<span data-ttu-id="00cdb-105">正常系統作業並不需要關閉 Microsoft Azure StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-105">Shutting down a Microsoft Azure StorSimple device is not required as a part of normal system operation.</span></span> <span data-ttu-id="00cdb-106">不過，您可能需要開啟新的裝置，或有裝置必須關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-106">However, you may need to turn on a new device or a device that had to be shut down.</span></span> <span data-ttu-id="00cdb-107">一般而言，在您需要更換故障的硬體、實際移動單元，或將裝置報廢的情況下才需要關機。</span><span class="sxs-lookup"><span data-stu-id="00cdb-107">Generally, a shutdown is required in cases in which you must replace failed hardware, physically move a unit, or take a device out of service.</span></span> <span data-ttu-id="00cdb-108">本教學課程將說明在不同案例中開啟和關閉 StorSimple 裝置的必要程序。</span><span class="sxs-lookup"><span data-stu-id="00cdb-108">This tutorial describes the required procedure for turning on and shutting down your StorSimple device in different scenarios.</span></span>

## <a name="turn-on-a-new-device"></a><span data-ttu-id="00cdb-109">開啟新的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-109">Turn on a new device</span></span>
<span data-ttu-id="00cdb-110">根據裝置型號是 8100 或 8600，初次開啟 StorSimple 裝置的步驟有所不同。</span><span class="sxs-lookup"><span data-stu-id="00cdb-110">The steps for turning on a StorSimple device for the first time differ depending on whether the device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="00cdb-111">8100 具有單一主要機箱，而 8600 是具有主要機箱與 EBOD 機箱的雙重機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-111">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="00cdb-112">下列各節涵蓋這兩個型號的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-112">The detailed steps for both models are covered in the following sections.</span></span>

* [<span data-ttu-id="00cdb-113">只有主要機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-113">New device with primary enclosure only</span></span>](#new-device-with-primary-enclosure-only)
* [<span data-ttu-id="00cdb-114">具有 EBOD 機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-114">New device with EBOD enclosure</span></span>](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a><span data-ttu-id="00cdb-115">只有主要機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-115">New device with primary enclosure only</span></span>
<span data-ttu-id="00cdb-116">StorSimple 8100 型是單一機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-116">The StorSimple 8100 model is a single enclosure device.</span></span> <span data-ttu-id="00cdb-117">您的裝置包含備援電源和冷卻模組 (PCM)。</span><span class="sxs-lookup"><span data-stu-id="00cdb-117">Your device includes redundant Power and Cooling Modules (PCMs).</span></span> <span data-ttu-id="00cdb-118">這兩個 PCM 都必須安裝，並且連接到不同的電源來源，以確保高可用性。</span><span class="sxs-lookup"><span data-stu-id="00cdb-118">Both PCMs must be installed and connected to different power sources to ensure high availability.</span></span>

<span data-ttu-id="00cdb-119">請執行下列步驟，以連接您的裝置的電源線。</span><span class="sxs-lookup"><span data-stu-id="00cdb-119">Perform the following steps to cable your device for power.</span></span>

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> <span data-ttu-id="00cdb-120">如需完成裝置設定和連接纜線的指示，請移至 [安裝您的 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="00cdb-120">For complete device setup and cabling instructions, go to [Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md).</span></span> <span data-ttu-id="00cdb-121">請確定有確實地依照指示進行。</span><span class="sxs-lookup"><span data-stu-id="00cdb-121">Make sure that you follow the instructions exactly.</span></span>
> 
> 

### <a name="new-device-with-ebod-enclosure"></a><span data-ttu-id="00cdb-122">具有 EBOD 機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-122">New device with EBOD enclosure</span></span>
<span data-ttu-id="00cdb-123">StorSimple 8600 型同時具有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-123">The StorSimple 8600 model has both a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="00cdb-124">這需要使用纜線將單元連接在一起，以取得序列連接 SCSI (SAS) 連線與電源。</span><span class="sxs-lookup"><span data-stu-id="00cdb-124">This requires the units to be cabled together for Serial Attached SCSI (SAS) connectivity and power.</span></span>

<span data-ttu-id="00cdb-125">第一次設定此裝置時，請先執行 SAS 佈線步驟，然後再完成電源佈線步驟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-125">When setting up this device for the first time, perform the steps for SAS cabling first and then complete the steps for power cabling.</span></span>

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> <span data-ttu-id="00cdb-126">如需完成裝置設定和連接纜線的指示，請移至 [安裝您的 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="00cdb-126">For complete device setup and cabling instructions, go to [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span> <span data-ttu-id="00cdb-127">請確定有確實地依照指示進行。</span><span class="sxs-lookup"><span data-stu-id="00cdb-127">Make sure that you follow the instructions exactly.</span></span>

## <a name="turn-on-a-device-after-shutdown"></a><span data-ttu-id="00cdb-128">在關機後開啟裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-128">Turn on a device after shutdown</span></span>
<span data-ttu-id="00cdb-129">根據裝置型號是 8100 或 8600，StorSimple 裝置關閉後再開啟它的步驟有所不同。</span><span class="sxs-lookup"><span data-stu-id="00cdb-129">The steps for turning on a StorSimple device after it has been shut down are different depending on whether the device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="00cdb-130">8100 具有單一主要機箱，而 8600 是具有主要機箱與 EBOD 機箱的雙重機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-130">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

* [<span data-ttu-id="00cdb-131">只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-131">Device with primary enclosure only</span></span>](#device-with-primary-enclosure-only)
* [<span data-ttu-id="00cdb-132">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-132">Device with EBOD enclosure</span></span>](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a><span data-ttu-id="00cdb-133">只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-133">Device with primary enclosure only</span></span>
<span data-ttu-id="00cdb-134">在關機之後，請使用下列程序來開啟只有主要機箱而沒有 EBOD 機箱的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-134">After a shutdown, use the following procedure to turn on a StorSimple device with a primary enclosure and no EBOD enclosure.</span></span>

#### <a name="to-turn-on-a-device-with-a-primary-enclosure-only"></a><span data-ttu-id="00cdb-135">若要開啟只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-135">To turn on a device with a primary enclosure only</span></span>
1. <span data-ttu-id="00cdb-136">請確定電源和冷卻模組 (PCM) 上的電源開關都在 OFF 的位置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-136">Make sure that the power switches on both Power and Cooling Modules (PCMs) are in the OFF position.</span></span> <span data-ttu-id="00cdb-137">如果開關不是在 OFF 的位置，請將它們切換到 OFF 的位置，並等候燈號熄滅。</span><span class="sxs-lookup"><span data-stu-id="00cdb-137">If the switches are not in the OFF position, then flip them to the OFF position and wait for the lights to go off.</span></span>
2. <span data-ttu-id="00cdb-138">將 PCM 上的電源開關都切換到 ON 的位置，開啟裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-138">Turn on the device by flipping the power switches on both PCMs to the ON position.</span></span> <span data-ttu-id="00cdb-139">裝置應該會開啟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-139">The device should turn on.</span></span>
3. <span data-ttu-id="00cdb-140">檢查下列項目來確認裝置是否完全開啟：</span><span class="sxs-lookup"><span data-stu-id="00cdb-140">Check the following to verify that the device is fully on:</span></span>
   
   1. <span data-ttu-id="00cdb-141">PCM 模組上的「OK」LED 燈號都是綠色。</span><span class="sxs-lookup"><span data-stu-id="00cdb-141">The OK LEDs on both PCM modules are green.</span></span>
   2. <span data-ttu-id="00cdb-142">控制器上的狀態 LED 燈號是持續的綠燈。</span><span class="sxs-lookup"><span data-stu-id="00cdb-142">The status LEDs on both controllers are solid green.</span></span>
   3. <span data-ttu-id="00cdb-143">其中一個控制器上的藍色 LED 燈號正在閃爍，指出控制器正作用中。</span><span class="sxs-lookup"><span data-stu-id="00cdb-143">The blue LED on one of the controllers is blinking, which indicates that the controller is active.</span></span>
      
      <span data-ttu-id="00cdb-144">如果有任何不符合上述的情況，則裝置的狀態不良。</span><span class="sxs-lookup"><span data-stu-id="00cdb-144">If any of these conditions are not met, then your device is not healthy.</span></span> <span data-ttu-id="00cdb-145">請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="00cdb-145">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="device-with-ebod-enclosure"></a><span data-ttu-id="00cdb-146">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-146">Device with EBOD enclosure</span></span>
<span data-ttu-id="00cdb-147">在關機之後，請使用下列程序來開啟具有主要機箱和 EBOD 機箱的 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-147">After a shutdown, use the following procedure to turn on a StorSimple device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="00cdb-148">請確實遵循說明依序執行每個步驟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-148">Perform each step in sequence exactly as described.</span></span> <span data-ttu-id="00cdb-149">若沒有這麼做，可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="00cdb-149">Failure to do so could result in data loss.</span></span>

#### <a name="to-turn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a><span data-ttu-id="00cdb-150">若要開啟具有主要和 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-150">To turn on a device with a primary and an EBOD enclosure</span></span>
1. <span data-ttu-id="00cdb-151">請確定 EBOD 機箱已經連接至主要機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-151">Make sure that the EBOD enclosure is connected to the primary enclosure.</span></span> <span data-ttu-id="00cdb-152">如需詳細資訊，請參閱 [安裝您的 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="00cdb-152">For more information, see [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="00cdb-153">請確定 EBOD 和主要機箱上的電源和冷卻模組 (PCM) 都在 OFF 的位置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-153">Make sure that the Power and Cooling Modules (PCMs) on both the EBOD and primary enclosures are in the OFF position.</span></span> <span data-ttu-id="00cdb-154">如果開關不是在 OFF 的位置，請將它們切換到 OFF 的位置，並等候燈號熄滅。</span><span class="sxs-lookup"><span data-stu-id="00cdb-154">If the switches are not in the OFF position, then flip them to the OFF position and wait for the lights to go off.</span></span>
3. <span data-ttu-id="00cdb-155">將 PCM 上的電源開關都切換到 ON 的位置，先開啟 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-155">Turn on the EBOD enclosure first by flipping the power switches on both PCMs to the ON position.</span></span> <span data-ttu-id="00cdb-156">PCM 的 LED 燈號應該是綠色。</span><span class="sxs-lookup"><span data-stu-id="00cdb-156">The PCM LEDs should be green.</span></span> <span data-ttu-id="00cdb-157">此單元上的 EBOD 控制器 LED 綠色燈號指出 EBOD 機箱已經開啟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-157">A green EBOD controller LED on this unit indicates that the EBOD enclosure is on.</span></span>
4. <span data-ttu-id="00cdb-158">將 PCM 上的電源開關都切換到 ON 的位置，開啟主要機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-158">Turn on the primary enclosure by flipping the power switches on both PCMs to the ON position.</span></span> <span data-ttu-id="00cdb-159">現在整個系統應該已經開啟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-159">The entire system should now be on.</span></span>
5. <span data-ttu-id="00cdb-160">確認 SAS LED 燈號都是綠色，確保 EBOD 機箱和主要機箱之間的連線狀態良好。</span><span class="sxs-lookup"><span data-stu-id="00cdb-160">Verify that the SAS LEDs are green, which ensures that the connection between the EBOD enclosure and the primary enclosure is good.</span></span>

## <a name="turn-on-a-device-after-a-power-loss"></a><span data-ttu-id="00cdb-161">在電源中斷後開啟裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-161">Turn on a device after a power loss</span></span>
<span data-ttu-id="00cdb-162">電源中斷會關閉 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-162">A power outage or interruption can shut down a StorSimple device.</span></span> <span data-ttu-id="00cdb-163">電源中斷可能會發生在其中一個電源供應器或同時發生在兩個電源供應器上。</span><span class="sxs-lookup"><span data-stu-id="00cdb-163">The power outage can happen on one of the power supplies or both power supplies.</span></span> <span data-ttu-id="00cdb-164">根據裝置型號是 8100 或 8600，復原步驟有所不同。</span><span class="sxs-lookup"><span data-stu-id="00cdb-164">The recovery steps are different depending on whether the device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="00cdb-165">8100 具有單一主要機箱，而 8600 是具有主要機箱與 EBOD 機箱的雙重機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-165">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="00cdb-166">本節將說明每個案例的修復程序。</span><span class="sxs-lookup"><span data-stu-id="00cdb-166">This section describes the recovery procedure for each scenario.</span></span>

* [<span data-ttu-id="00cdb-167">只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-167">Device with primary enclosure only</span></span>](#8100)
* [<span data-ttu-id="00cdb-168">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-168">Device with EBOD enclosure</span></span>](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a><span data-ttu-id="00cdb-169">只有主要機箱的裝置 <a name="8100"></span><span class="sxs-lookup"><span data-stu-id="00cdb-169">Device with primary enclosure only <a name="8100"></span></span>
<span data-ttu-id="00cdb-170">如果其中一個電源供應器的電源中斷，系統還是可以繼續正常作業。</span><span class="sxs-lookup"><span data-stu-id="00cdb-170">The system can continue its normal operation if there is power loss to one of its power supplies.</span></span> <span data-ttu-id="00cdb-171">不過，為確保裝置的高可用性，請儘速恢復電源供應器的電源。</span><span class="sxs-lookup"><span data-stu-id="00cdb-171">However, to ensure high availability of the device, restore power to the power supply as soon as possible.</span></span>

<span data-ttu-id="00cdb-172">如果同時在兩個電源供應器上發生電源中斷，系統會以有條理的方式關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-172">If there is a power outage or power interruption on both power supplies, the system will shut down in an orderly and controlled manner.</span></span> <span data-ttu-id="00cdb-173">當電源恢復時，系統將會自動開啟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-173">When the power is restored, the system will automatically turn on.</span></span>

### <a name="device-with-ebod-enclosure-a-name8600"></a><span data-ttu-id="00cdb-174">具有 EBOD 機箱的裝置 <a name="8600"></span><span class="sxs-lookup"><span data-stu-id="00cdb-174">Device with EBOD enclosure <a name="8600"></span></span>
#### <a name="power-loss-on-one-power-supply"></a><span data-ttu-id="00cdb-175">單一電源供應器電源中斷</span><span class="sxs-lookup"><span data-stu-id="00cdb-175">Power loss on one power supply</span></span>
<span data-ttu-id="00cdb-176">如果主要機箱或 EBOD 機箱的其中一個電源供應器電源中斷，系統還是可以繼續正常作業。</span><span class="sxs-lookup"><span data-stu-id="00cdb-176">The system can continue its normal operation if there is power loss to one of its power supplies on the primary enclosure or the EBOD enclosure.</span></span> <span data-ttu-id="00cdb-177">不過，為確保裝置的高可用性，請儘速恢復電源供應器的電源。</span><span class="sxs-lookup"><span data-stu-id="00cdb-177">However, to ensure high availability of the device, please restore power to the power supply as soon as possible.</span></span>

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a><span data-ttu-id="00cdb-178">主要機箱和 EBOD 機箱的電源供應器同時電源中斷</span><span class="sxs-lookup"><span data-stu-id="00cdb-178">Power loss on both power supplies on primary and EBOD enclosures</span></span>
<span data-ttu-id="00cdb-179">如果同時在兩個電源供應器上發生電源中斷，EBOD 機箱將會立即關閉，而主要機箱會以有條理的方式關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-179">If there is a power outage or power interruption on both power supplies, the EBOD enclosure will shut down immediately and the primary enclosure will shut down in an orderly and controlled manner.</span></span> <span data-ttu-id="00cdb-180">當電源恢復時，應用裝置會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="00cdb-180">When power is restored, the appliance will start automatically.</span></span>

<span data-ttu-id="00cdb-181">如果電源是以手動方式關閉，則執行下列步驟來恢復系統的電源。</span><span class="sxs-lookup"><span data-stu-id="00cdb-181">If the power is switched off manually, then take the following steps to restore power to the system.</span></span>

1. <span data-ttu-id="00cdb-182">開啟 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-182">Turn on the EBOD enclosure.</span></span>
2. <span data-ttu-id="00cdb-183">在 EBOD 機箱開啟之後，開啟主要機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-183">After the EBOD enclosure is on, turn on the primary enclosure.</span></span>

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a><span data-ttu-id="00cdb-184">EBOD 機箱上的兩個電源供應器同時電源中斷</span><span class="sxs-lookup"><span data-stu-id="00cdb-184">Power loss on both power supplies on EBOD enclosure</span></span>
<span data-ttu-id="00cdb-185">當安裝纜線時，您必須確定 EBOD 機箱絕對不會單獨連接至個別的 PDU。</span><span class="sxs-lookup"><span data-stu-id="00cdb-185">When you set up your cables, you must ensure that the EBOD is never connected alone to a separate PDU.</span></span> <span data-ttu-id="00cdb-186">如果 EBOD 和主要機箱同時故障，系統將會復原。</span><span class="sxs-lookup"><span data-stu-id="00cdb-186">If the EBOD and primary enclosure fail at the same time, the system will recover.</span></span>

<span data-ttu-id="00cdb-187">如果只有 EBOD 機箱的兩個電源供應器同時故障，系統將不會自動復原。</span><span class="sxs-lookup"><span data-stu-id="00cdb-187">If only the EBOD enclosure fails on both power supplies, the system will not automatically recover.</span></span> <span data-ttu-id="00cdb-188">執行下列步驟開啟系統並將其還原至良好狀態：</span><span class="sxs-lookup"><span data-stu-id="00cdb-188">Take the following steps to turn on the system and restore it to a healthy state:</span></span>

1. <span data-ttu-id="00cdb-189">如果主要機箱已經開啟，請將電源和冷卻模組 (PCM) 關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-189">If the primary enclosure is turned on, switch off both Power and Cooling Modules (PCMs).</span></span>
2. <span data-ttu-id="00cdb-190">請等候幾分鐘，讓系統關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-190">Wait for a few minutes for the system to shut down.</span></span>
3. <span data-ttu-id="00cdb-191">開啟 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-191">Turn on the EBOD enclosure.</span></span>
4. <span data-ttu-id="00cdb-192">在 EBOD 機箱開啟之後，開啟主要機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-192">After the EBOD enclosure is on, turn on the primary enclosure.</span></span>

## <a name="turn-on-a-device-after-the-primary-and-ebod-enclosure-connection-is-lost"></a><span data-ttu-id="00cdb-193">在主要機箱和 EBOD 機箱連線中斷後開啟裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-193">Turn on a device after the primary and EBOD enclosure connection is lost</span></span>
<span data-ttu-id="00cdb-194">如果待命控制器與對應的 EBOD 控制器連線中斷，裝置仍會繼續運作。</span><span class="sxs-lookup"><span data-stu-id="00cdb-194">If the connection is lost between the standby controller and the corresponding EBOD controller, the device continues to work.</span></span> <span data-ttu-id="00cdb-195">如果系統作用中的控制器和對應的 EBOD 控制器連線中斷，則應該會進行容錯移轉且裝置應該會繼續正常運作。</span><span class="sxs-lookup"><span data-stu-id="00cdb-195">If the connection between the system active controller and the corresponding EBOD controller is lost, failover should occur and the device should continue to work as normal.</span></span>

<span data-ttu-id="00cdb-196">當移除兩條序列連接 SCSI (SAS) 纜線，或切斷 EBOD 機箱與主要機箱間的連線，裝置將會停止運作。</span><span class="sxs-lookup"><span data-stu-id="00cdb-196">When both Serial Attached SCSI (SAS) cables are removed or the connection between the EBOD enclosure and the primary enclosure is severed, the device will stop working.</span></span> <span data-ttu-id="00cdb-197">此時請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-197">At this point, perform the following steps.</span></span>

### <a name="to-turn-on-the-device-after-connection-is-lost"></a><span data-ttu-id="00cdb-198">若要在連線中斷後開啟裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-198">To turn on the device after connection is lost</span></span>
1. <span data-ttu-id="00cdb-199">進入裝置的背面。</span><span class="sxs-lookup"><span data-stu-id="00cdb-199">Access the back of the device.</span></span>
2. <span data-ttu-id="00cdb-200">如果在 EBOD 機箱和主要機箱間的 SAS 纜線連線損毀，EBOD 機箱上所有的 SAS 通道 LED 燈號將會關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-200">If the SAS cable connection between the EBOD enclosure and the primary enclosure is broken, all SAS lane LEDs on the EBOD enclosure will be off.</span></span>
3. <span data-ttu-id="00cdb-201">關閉 EBOD 機箱和主要機箱上的電源和冷卻模組 (PCM)。</span><span class="sxs-lookup"><span data-stu-id="00cdb-201">Shut down both Power and Cooling Modules (PCMs) on the EBOD enclosure and the primary enclosure.</span></span>
4. <span data-ttu-id="00cdb-202">等候兩個機箱背面的所有燈號關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-202">Wait until all the lights on the back of both the enclosures turn off.</span></span>
5. <span data-ttu-id="00cdb-203">重新插入 SAS 纜線，並確定在 EBOD 機箱和主要機箱間有良好的連線。</span><span class="sxs-lookup"><span data-stu-id="00cdb-203">Reinsert the SAS cables, and ensure that there is a good connection between the EBOD enclosure and the primary enclosure.</span></span>
6. <span data-ttu-id="00cdb-204">將 PCM 上的開關都切換到 ON 的位置，先開啟 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-204">Turn on the EBOD enclosure first by flipping both PCM switches to the ON position.</span></span>
7. <span data-ttu-id="00cdb-205">檢查綠色 LED 燈號是否亮起，確定 EBOD 機箱已經開啟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-205">Ensure that the EBOD enclosure is on by checking that the green LED is ON.</span></span>
8. <span data-ttu-id="00cdb-206">開啟主要機箱。</span><span class="sxs-lookup"><span data-stu-id="00cdb-206">Turn on the primary enclosure.</span></span>
9. <span data-ttu-id="00cdb-207">透過檢查控制器綠色 LED 燈號是否亮起，確定主要機箱已經開啟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-207">Ensure that the primary enclosure is on by checking that the controller green LED is ON.</span></span>
10. <span data-ttu-id="00cdb-208">透過檢查 SAS 通道 LED 燈號 (每個 EBOD 控制器有 4 個) 全部亮起，確認 EBOD 機箱與主要機箱間的連線良好。</span><span class="sxs-lookup"><span data-stu-id="00cdb-208">Verify that the EBOD enclosure connection with the primary enclosure is good by checking that the SAS lane LEDs (four per EBOD controller) are all ON.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00cdb-209">如果 SAS 纜線損壞，或是 EBOD 機箱和主要機箱間的連線不佳，則當您開啟系統時，會進入修復模式。</span><span class="sxs-lookup"><span data-stu-id="00cdb-209">If the SAS cables are defective or the connection between the EBOD enclosure and the primary enclosure is not good, when you turn on the system, it will go into recovery mode.</span></span> <span data-ttu-id="00cdb-210">如果發生此情況，請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) 。</span><span class="sxs-lookup"><span data-stu-id="00cdb-210">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) if this happens.</span></span>


## <a name="turn-off-a-running-device"></a><span data-ttu-id="00cdb-211">關閉執行中的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-211">Turn off a running device</span></span>
<span data-ttu-id="00cdb-212">如果執行中的 StorSimple 裝置需要移動、報廢，或是更換運作失常的元件，就可能需要關機。</span><span class="sxs-lookup"><span data-stu-id="00cdb-212">A running StorSimple device may need to be shut down if it is being moved, taken out of service, or has a malfunctioning component that needs to be replaced.</span></span> <span data-ttu-id="00cdb-213">根據 StorSimple 裝置的型號是 8100 或 8600，步驟會有所不同。</span><span class="sxs-lookup"><span data-stu-id="00cdb-213">The steps are different depending on whether the StorSimple device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="00cdb-214">8100 具有單一主要機箱，而 8600 是具有主要機箱與 EBOD 機箱的雙重機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-214">The 8100 has a single primary enclosure, whereas the 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="00cdb-215">本節將詳細說明關閉執行中裝置的步驟。</span><span class="sxs-lookup"><span data-stu-id="00cdb-215">This section details the steps to shut down a running device.</span></span>

* [<span data-ttu-id="00cdb-216">具有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-216">Device with primary enclosure</span></span>](#8100a)
* [<span data-ttu-id="00cdb-217">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-217">Device with EBOD enclosure</span></span>](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a><span data-ttu-id="00cdb-218">具有主要機箱的裝置 <a name="8100a"></span><span class="sxs-lookup"><span data-stu-id="00cdb-218">Device with primary enclosure <a name="8100a"></span></span>
<span data-ttu-id="00cdb-219">若要依序且以受控制的方式關閉裝置，您可以透過 Azure 傳統入口網站或透過 Windows PowerShell for StorSimple 來執行。</span><span class="sxs-lookup"><span data-stu-id="00cdb-219">To shut down the device in an orderly and controlled manner, you can do it through the Azure classic portal or via the Windows PowerShell for StorSimple.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="00cdb-220">請勿使用裝置背面的電源按鈕關閉執行中的裝置。</span><span class="sxs-lookup"><span data-stu-id="00cdb-220">Do not shut down a running device by using the power button on the back of the device.</span></span>
> 
> <span data-ttu-id="00cdb-221">關閉裝置之前，請確定所有的裝置元件狀態良好。</span><span class="sxs-lookup"><span data-stu-id="00cdb-221">Before shutting down the device, make sure that all the device components are healthy.</span></span> <span data-ttu-id="00cdb-222">在 Azure 傳統入口網站中，瀏覽至 [裝置]  >  [維護]  >  [硬體狀態]，並確認所有的元件狀態是綠色的。</span><span class="sxs-lookup"><span data-stu-id="00cdb-222">In the Azure classic portal, navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that status of all the components is green.</span></span> <span data-ttu-id="00cdb-223">這只適用於狀態良好的系統。</span><span class="sxs-lookup"><span data-stu-id="00cdb-223">This is true only for a healthy system.</span></span> <span data-ttu-id="00cdb-224">如果系統正在關閉中以更換故障的元件，您會在 [硬體狀態] 中看到個別元件的失敗 (紅色) 或降級 (黃色) 狀態。</span><span class="sxs-lookup"><span data-stu-id="00cdb-224">If the system is being shut down to replace a malfunctioning component, you will see a failed (red) or degraded (yellow) status for the respective component in the **Hardware Status**.</span></span>
> 
> 

<span data-ttu-id="00cdb-225">存取 Windows PowerShell for StorSimple 或 Azure 傳統入口網站之後，請依照 [關閉 StorSimple 裝置](storsimple-manage-device-controller.md#shut-down-a-storsimple-device)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="00cdb-225">After you access the Windows PowerShell for StorSimple or the Azure classic portal, follow the steps in [shut down a StorSimple device](storsimple-manage-device-controller.md#shut-down-a-storsimple-device).</span></span> 

### <a name="device-with-ebod-enclosure-a-name8600a"></a><span data-ttu-id="00cdb-226">具有 EBOD 機箱的裝置 <a name="8600a"></span><span class="sxs-lookup"><span data-stu-id="00cdb-226">Device with EBOD enclosure <a name="8600a"></span></span>
> [!IMPORTANT]
> <span data-ttu-id="00cdb-227">關閉主要機箱和 EBOD 機箱之前，請確定所有裝置元件狀態良好。</span><span class="sxs-lookup"><span data-stu-id="00cdb-227">Before shutting down the primary enclosure and the EBOD enclosure, ensure that all the device components are healthy.</span></span> <span data-ttu-id="00cdb-228">在 Azure 入口網站中，瀏覽至 [裝置]  > [監視]  >  [硬體健康狀態]，確認所有的元件狀態都良好。</span><span class="sxs-lookup"><span data-stu-id="00cdb-228">In the Azure portal, navigate to **Devices** > **Monitor** > **Hardware health**, and verify that all the components are healthy.</span></span>


#### <a name="to-shut-down-a-running-device-with-ebod-enclosure"></a><span data-ttu-id="00cdb-229">若要關閉具有 EBOD 機箱的執行中裝置</span><span class="sxs-lookup"><span data-stu-id="00cdb-229">To shut down a running device with EBOD enclosure</span></span>
1. <span data-ttu-id="00cdb-230">針對主要機箱，請依照 [關閉 StorSimple 裝置](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) 中列出的所有步驟執行。</span><span class="sxs-lookup"><span data-stu-id="00cdb-230">Follow all the steps listed in [shut down a StorSimple device](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) for the primary enclosure.</span></span>
2. <span data-ttu-id="00cdb-231">關閉主要機箱之後，將電源和冷卻模組 (PCM) 的開關都切換至 OFF 以關閉 EBOD。</span><span class="sxs-lookup"><span data-stu-id="00cdb-231">After the primary enclosure is shut down, shut down the EBOD by flipping off both Power and Cooling Module (PCM) switches.</span></span>
3. <span data-ttu-id="00cdb-232">若要確認 EBOD 已關閉，請檢查 EBOD 機箱背面的所有燈號都已關閉。</span><span class="sxs-lookup"><span data-stu-id="00cdb-232">To verify that the EBOD has shut down, check that all lights on the back of the EBOD enclosure are off.</span></span>

> [!NOTE]
> <span data-ttu-id="00cdb-233">SAS 纜線是用來連接 EBOD 機箱與主要機箱，且在系統關閉之前都不應該移除。</span><span class="sxs-lookup"><span data-stu-id="00cdb-233">The SAS cables that are used to connect the EBOD enclosure to the primary enclosure should not be removed until after the system is shut down.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00cdb-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00cdb-234">Next steps</span></span>
<span data-ttu-id="00cdb-235">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) 。</span><span class="sxs-lookup"><span data-stu-id="00cdb-235">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) if you encounter problems when turning on or shutting down a StorSimple device.</span></span>

