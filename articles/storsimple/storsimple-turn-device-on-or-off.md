---
title: "aaaTurn StorSimple 8000 系列裝置開啟或關閉 |Microsoft 文件"
description: "說明如何在新的 StorSimple 裝置，tooturn 開啟的裝置已關閉或失去電源，並關閉執行中的裝置。"
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
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a><span data-ttu-id="3bd06-103">開啟或關閉 StorSimple 8000 系列裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-103">Turn on or turn off your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="3bd06-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3bd06-104">Overview</span></span>
<span data-ttu-id="3bd06-105">正常系統作業並不需要關閉 Microsoft Azure StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-105">Shutting down a Microsoft Azure StorSimple device is not required as a part of normal system operation.</span></span> <span data-ttu-id="3bd06-106">不過，您可能需要新的裝置或裝置已關閉的 toobe tooturn。</span><span class="sxs-lookup"><span data-stu-id="3bd06-106">However, you may need tooturn on a new device or a device that had toobe shut down.</span></span> <span data-ttu-id="3bd06-107">一般而言，在您需要更換故障的硬體、實際移動單元，或將裝置報廢的情況下才需要關機。</span><span class="sxs-lookup"><span data-stu-id="3bd06-107">Generally, a shutdown is required in cases in which you must replace failed hardware, physically move a unit, or take a device out of service.</span></span> <span data-ttu-id="3bd06-108">本教學課程說明開啟和關閉您的 StorSimple 裝置在不同案例中的所需的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="3bd06-108">This tutorial describes hello required procedure for turning on and shutting down your StorSimple device in different scenarios.</span></span>

## <a name="turn-on-a-new-device"></a><span data-ttu-id="3bd06-109">開啟新的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-109">Turn on a new device</span></span>
<span data-ttu-id="3bd06-110">hello 第一次開啟 hello StorSimple 裝置的步驟有所不同 hello 裝置是否 8100 或 8600 模型。</span><span class="sxs-lookup"><span data-stu-id="3bd06-110">hello steps for turning on a StorSimple device for hello first time differ depending on whether hello device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="3bd06-111">hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-111">hello 8100 has a single primary enclosure, whereas hello 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="3bd06-112">hello 這兩個模型的詳細的步驟涵蓋下列各節的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bd06-112">hello detailed steps for both models are covered in hello following sections.</span></span>

* [<span data-ttu-id="3bd06-113">只有主要機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-113">New device with primary enclosure only</span></span>](#new-device-with-primary-enclosure-only)
* [<span data-ttu-id="3bd06-114">具有 EBOD 機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-114">New device with EBOD enclosure</span></span>](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a><span data-ttu-id="3bd06-115">只有主要機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-115">New device with primary enclosure only</span></span>
<span data-ttu-id="3bd06-116">hello StorSimple 8100 模型是單一機箱裝置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-116">hello StorSimple 8100 model is a single enclosure device.</span></span> <span data-ttu-id="3bd06-117">您的裝置包含備援電源和冷卻模組 (PCM)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-117">Your device includes redundant Power and Cooling Modules (PCMs).</span></span> <span data-ttu-id="3bd06-118">這兩個 Pcm 必須安裝並連接 toodifferent 電源來源 tooensure 高可用性。</span><span class="sxs-lookup"><span data-stu-id="3bd06-118">Both PCMs must be installed and connected toodifferent power sources tooensure high availability.</span></span>

<span data-ttu-id="3bd06-119">執行您的裝置 hello 遵循步驟 toocable 電源。</span><span class="sxs-lookup"><span data-stu-id="3bd06-119">Perform hello following steps toocable your device for power.</span></span>

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> <span data-ttu-id="3bd06-120">完成裝置設定和纜線連接指示，請移過[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-120">For complete device setup and cabling instructions, go too[Install your StorSimple 8100 device](storsimple-8100-hardware-installation.md).</span></span> <span data-ttu-id="3bd06-121">請確定您確實依照 hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="3bd06-121">Make sure that you follow hello instructions exactly.</span></span>
> 
> 

### <a name="new-device-with-ebod-enclosure"></a><span data-ttu-id="3bd06-122">具有 EBOD 機箱的新裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-122">New device with EBOD enclosure</span></span>
<span data-ttu-id="3bd06-123">hello StorSimple 8600 模型有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-123">hello StorSimple 8600 model has both a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="3bd06-124">這需要 hello 單位 toobe 接上一起取得序列連接 SCSI (SAS) 連線和電源。</span><span class="sxs-lookup"><span data-stu-id="3bd06-124">This requires hello units toobe cabled together for Serial Attached SCSI (SAS) connectivity and power.</span></span>

<span data-ttu-id="3bd06-125">設定此裝置 hello 第一次，請執行 hello 步驟 SAS 佈線第一次，然後完成 hello 電源佈線的步驟。</span><span class="sxs-lookup"><span data-stu-id="3bd06-125">When setting up this device for hello first time, perform hello steps for SAS cabling first and then complete hello steps for power cabling.</span></span>

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> <span data-ttu-id="3bd06-126">完成裝置設定和纜線連接指示，請移過[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-126">For complete device setup and cabling instructions, go too[Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span> <span data-ttu-id="3bd06-127">請確定您確實依照 hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="3bd06-127">Make sure that you follow hello instructions exactly.</span></span>

## <a name="turn-on-a-device-after-shutdown"></a><span data-ttu-id="3bd06-128">在關機後開啟裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-128">Turn on a device after shutdown</span></span>
<span data-ttu-id="3bd06-129">它已關閉後開啟 StorSimple 裝置 hello 步驟會有所不同 hello 裝置是否 8100 或 8600 模型項目。</span><span class="sxs-lookup"><span data-stu-id="3bd06-129">hello steps for turning on a StorSimple device after it has been shut down are different depending on whether hello device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="3bd06-130">hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-130">hello 8100 has a single primary enclosure, whereas hello 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span>

* [<span data-ttu-id="3bd06-131">只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-131">Device with primary enclosure only</span></span>](#device-with-primary-enclosure-only)
* [<span data-ttu-id="3bd06-132">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-132">Device with EBOD enclosure</span></span>](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a><span data-ttu-id="3bd06-133">只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-133">Device with primary enclosure only</span></span>
<span data-ttu-id="3bd06-134">關閉後，使用下列程序 tooturn StorSimple 裝置沒有 EBOD 機箱與主要機箱上的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bd06-134">After a shutdown, use hello following procedure tooturn on a StorSimple device with a primary enclosure and no EBOD enclosure.</span></span>

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a><span data-ttu-id="3bd06-135">只有主要機箱的裝置上的 tooturn</span><span class="sxs-lookup"><span data-stu-id="3bd06-135">tooturn on a device with a primary enclosure only</span></span>
1. <span data-ttu-id="3bd06-136">請確定，hello 電源開關這兩個電源和冷卻模組 (Pcm) 是在 hello OFF 位置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-136">Make sure that hello power switches on both Power and Cooling Modules (PCMs) are in hello OFF position.</span></span> <span data-ttu-id="3bd06-137">如果 hello 參數不在 hello 關閉 」 位置，然後翻轉 toohello 關閉 」 位置，並等待 hello 燈號 toogo 關閉。</span><span class="sxs-lookup"><span data-stu-id="3bd06-137">If hello switches are not in hello OFF position, then flip them toohello OFF position and wait for hello lights toogo off.</span></span>
2. <span data-ttu-id="3bd06-138">開啟 hello 裝置 hello 電源開關 」 這兩個 Pcm toohello 開啟 」 位置上。</span><span class="sxs-lookup"><span data-stu-id="3bd06-138">Turn on hello device by flipping hello power switches on both PCMs toohello ON position.</span></span> <span data-ttu-id="3bd06-139">hello 裝置應開啟。</span><span class="sxs-lookup"><span data-stu-id="3bd06-139">hello device should turn on.</span></span>
3. <span data-ttu-id="3bd06-140">核取 hello 遵循 hello 裝置的 tooverify 已完全開啟：</span><span class="sxs-lookup"><span data-stu-id="3bd06-140">Check hello following tooverify that hello device is fully on:</span></span>
   
   1. <span data-ttu-id="3bd06-141">這兩個 PCM 模組上的 hello 正常 Led 」 皆為綠色。</span><span class="sxs-lookup"><span data-stu-id="3bd06-141">hello OK LEDs on both PCM modules are green.</span></span>
   2. <span data-ttu-id="3bd06-142">兩個控制器上的 hello 狀態 led 皆為純綠色。</span><span class="sxs-lookup"><span data-stu-id="3bd06-142">hello status LEDs on both controllers are solid green.</span></span>
   3. <span data-ttu-id="3bd06-143">hello 其中一個 hello 控制站上的藍色 LED 閃爍不停，這表示該 hello 控制器為作用中。</span><span class="sxs-lookup"><span data-stu-id="3bd06-143">hello blue LED on one of hello controllers is blinking, which indicates that hello controller is active.</span></span>
      
      <span data-ttu-id="3bd06-144">如果有任何不符合上述的情況，則裝置的狀態不良。</span><span class="sxs-lookup"><span data-stu-id="3bd06-144">If any of these conditions are not met, then your device is not healthy.</span></span> <span data-ttu-id="3bd06-145">請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-145">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="device-with-ebod-enclosure"></a><span data-ttu-id="3bd06-146">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-146">Device with EBOD enclosure</span></span>
<span data-ttu-id="3bd06-147">關閉後，使用下列程序 tooturn StorSimple 裝置主要機箱與 EBOD 機箱上的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bd06-147">After a shutdown, use hello following procedure tooturn on a StorSimple device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="3bd06-148">請確實遵循說明依序執行每個步驟。</span><span class="sxs-lookup"><span data-stu-id="3bd06-148">Perform each step in sequence exactly as described.</span></span> <span data-ttu-id="3bd06-149">失敗 toodo 因此可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="3bd06-149">Failure toodo so could result in data loss.</span></span>

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a><span data-ttu-id="3bd06-150">tooturn 主要和 EBOD 機箱的裝置上</span><span class="sxs-lookup"><span data-stu-id="3bd06-150">tooturn on a device with a primary and an EBOD enclosure</span></span>
1. <span data-ttu-id="3bd06-151">請確定該 hello EBOD 機箱已連接的 toohello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-151">Make sure that hello EBOD enclosure is connected toohello primary enclosure.</span></span> <span data-ttu-id="3bd06-152">如需詳細資訊，請參閱 [安裝您的 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-152">For more information, see [Install your StorSimple 8600 device](storsimple-8600-hardware-installation.md).</span></span>
2. <span data-ttu-id="3bd06-153">請確定該 hello 電源和冷卻模組 (Pcm) 上同時 hello EBOD 與主要機箱已 hello OFF 位置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-153">Make sure that hello Power and Cooling Modules (PCMs) on both hello EBOD and primary enclosures are in hello OFF position.</span></span> <span data-ttu-id="3bd06-154">如果 hello 參數不在 hello 關閉 」 位置，然後翻轉 toohello 關閉 」 位置，並等待 hello 燈號 toogo 關閉。</span><span class="sxs-lookup"><span data-stu-id="3bd06-154">If hello switches are not in hello OFF position, then flip them toohello OFF position and wait for hello lights toogo off.</span></span>
3. <span data-ttu-id="3bd06-155">開啟 EBOD 機箱 hello 第一個翻轉 hello 電源開關都在這兩個 Pcm toohello 開啟 」 位置上。</span><span class="sxs-lookup"><span data-stu-id="3bd06-155">Turn on hello EBOD enclosure first by flipping hello power switches on both PCMs toohello ON position.</span></span> <span data-ttu-id="3bd06-156">hello PCM Led 應為綠色。</span><span class="sxs-lookup"><span data-stu-id="3bd06-156">hello PCM LEDs should be green.</span></span> <span data-ttu-id="3bd06-157">此裝置上的綠色 EBOD 控制器 LED 表示 hello EBOD 機箱已開啟。</span><span class="sxs-lookup"><span data-stu-id="3bd06-157">A green EBOD controller LED on this unit indicates that hello EBOD enclosure is on.</span></span>
4. <span data-ttu-id="3bd06-158">開啟主要機箱 hello 翻轉 hello 電源開關都在這兩個 Pcm toohello 開啟 」 位置上。</span><span class="sxs-lookup"><span data-stu-id="3bd06-158">Turn on hello primary enclosure by flipping hello power switches on both PCMs toohello ON position.</span></span> <span data-ttu-id="3bd06-159">hello 整個系統現在應該亮起。</span><span class="sxs-lookup"><span data-stu-id="3bd06-159">hello entire system should now be on.</span></span>
5. <span data-ttu-id="3bd06-160">請確認 hello SAS Led 為綠色，並確保該 hello 之間的連線 hello EBOD 機箱 hello 主要機箱是理想的狀況。</span><span class="sxs-lookup"><span data-stu-id="3bd06-160">Verify that hello SAS LEDs are green, which ensures that hello connection between hello EBOD enclosure and hello primary enclosure is good.</span></span>

## <a name="turn-on-a-device-after-a-power-loss"></a><span data-ttu-id="3bd06-161">在電源中斷後開啟裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-161">Turn on a device after a power loss</span></span>
<span data-ttu-id="3bd06-162">電源中斷會關閉 StorSimple 裝置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-162">A power outage or interruption can shut down a StorSimple device.</span></span> <span data-ttu-id="3bd06-163">hello 斷電情形 hello 電源供應器的其中一個或兩個電源供應器上。</span><span class="sxs-lookup"><span data-stu-id="3bd06-163">hello power outage can happen on one of hello power supplies or both power supplies.</span></span> <span data-ttu-id="3bd06-164">hello 復原步驟會有所不同 hello 裝置是否 8100 或 8600 模型項目。</span><span class="sxs-lookup"><span data-stu-id="3bd06-164">hello recovery steps are different depending on whether hello device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="3bd06-165">hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-165">hello 8100 has a single primary enclosure, whereas hello 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="3bd06-166">本節說明每個案例中的 hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="3bd06-166">This section describes hello recovery procedure for each scenario.</span></span>

* [<span data-ttu-id="3bd06-167">只有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-167">Device with primary enclosure only</span></span>](#8100)
* [<span data-ttu-id="3bd06-168">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-168">Device with EBOD enclosure</span></span>](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a><span data-ttu-id="3bd06-169">只有主要機箱的裝置 <a name="8100"></span><span class="sxs-lookup"><span data-stu-id="3bd06-169">Device with primary enclosure only <a name="8100"></span></span>
<span data-ttu-id="3bd06-170">如果有一個電源供應器的電源遺失 tooone hello 系統可以繼續其正常作業。</span><span class="sxs-lookup"><span data-stu-id="3bd06-170">hello system can continue its normal operation if there is power loss tooone of its power supplies.</span></span> <span data-ttu-id="3bd06-171">不過，tooensure 高可用性的 hello 裝置，還原電源 toohello 電源供應器儘速。</span><span class="sxs-lookup"><span data-stu-id="3bd06-171">However, tooensure high availability of hello device, restore power toohello power supply as soon as possible.</span></span>

<span data-ttu-id="3bd06-172">如果沒有電源中斷或兩個電源供應器的電源中斷，hello 系統將會關閉以井然有序且受控制的方式。</span><span class="sxs-lookup"><span data-stu-id="3bd06-172">If there is a power outage or power interruption on both power supplies, hello system will shut down in an orderly and controlled manner.</span></span> <span data-ttu-id="3bd06-173">還原 hello 電源時，將會自動開啟 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="3bd06-173">When hello power is restored, hello system will automatically turn on.</span></span>

### <a name="device-with-ebod-enclosure-a-name8600"></a><span data-ttu-id="3bd06-174">具有 EBOD 機箱的裝置 <a name="8600"></span><span class="sxs-lookup"><span data-stu-id="3bd06-174">Device with EBOD enclosure <a name="8600"></span></span>
#### <a name="power-loss-on-one-power-supply"></a><span data-ttu-id="3bd06-175">單一電源供應器電源中斷</span><span class="sxs-lookup"><span data-stu-id="3bd06-175">Power loss on one power supply</span></span>
<span data-ttu-id="3bd06-176">如果有一個主要機箱 hello 或 hello EBOD 機箱上的電源供應器的電源遺失 tooone hello 系統可以繼續其正常作業。</span><span class="sxs-lookup"><span data-stu-id="3bd06-176">hello system can continue its normal operation if there is power loss tooone of its power supplies on hello primary enclosure or hello EBOD enclosure.</span></span> <span data-ttu-id="3bd06-177">不過，tooensure 高可用性的 hello 裝置，請還原電源 toohello 電源供應器儘速。</span><span class="sxs-lookup"><span data-stu-id="3bd06-177">However, tooensure high availability of hello device, please restore power toohello power supply as soon as possible.</span></span>

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a><span data-ttu-id="3bd06-178">主要機箱和 EBOD 機箱的電源供應器同時電源中斷</span><span class="sxs-lookup"><span data-stu-id="3bd06-178">Power loss on both power supplies on primary and EBOD enclosures</span></span>
<span data-ttu-id="3bd06-179">如果沒有這兩個電源供應器都有電源中斷或電源中斷，hello EBOD 機箱將立即關閉，並以井然有序且受控制的方式將關閉 hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-179">If there is a power outage or power interruption on both power supplies, hello EBOD enclosure will shut down immediately and hello primary enclosure will shut down in an orderly and controlled manner.</span></span> <span data-ttu-id="3bd06-180">當電源恢復時，會自動啟動 hello 應用裝置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-180">When power is restored, hello appliance will start automatically.</span></span>

<span data-ttu-id="3bd06-181">如果以手動方式關閉 hello 電源，然後採取下列步驟 toorestore 電源 toohello 系統 hello。</span><span class="sxs-lookup"><span data-stu-id="3bd06-181">If hello power is switched off manually, then take hello following steps toorestore power toohello system.</span></span>

1. <span data-ttu-id="3bd06-182">開啟 hello EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-182">Turn on hello EBOD enclosure.</span></span>
2. <span data-ttu-id="3bd06-183">Hello EBOD 機箱上 」 之後，請開啟 hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-183">After hello EBOD enclosure is on, turn on hello primary enclosure.</span></span>

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a><span data-ttu-id="3bd06-184">EBOD 機箱上的兩個電源供應器同時電源中斷</span><span class="sxs-lookup"><span data-stu-id="3bd06-184">Power loss on both power supplies on EBOD enclosure</span></span>
<span data-ttu-id="3bd06-185">當您設定您的纜線時，您必須確定 EBOD 絕不會是該 hello 連接單獨 tooa 個別 PDU。</span><span class="sxs-lookup"><span data-stu-id="3bd06-185">When you set up your cables, you must ensure that hello EBOD is never connected alone tooa separate PDU.</span></span> <span data-ttu-id="3bd06-186">如果在 hello 失敗的 hello EBOD 與主要機箱 hello 系統將復原相同的時間。</span><span class="sxs-lookup"><span data-stu-id="3bd06-186">If hello EBOD and primary enclosure fail at hello same time, hello system will recover.</span></span>

<span data-ttu-id="3bd06-187">如果只有 EBOD 機箱 hello 失敗這兩個電源供應器，hello 系統將不會自動復原。</span><span class="sxs-lookup"><span data-stu-id="3bd06-187">If only hello EBOD enclosure fails on both power supplies, hello system will not automatically recover.</span></span> <span data-ttu-id="3bd06-188">採用 hello 遵循步驟 tooturn hello 系統上，並將它還原 tooa 狀況良好的狀態：</span><span class="sxs-lookup"><span data-stu-id="3bd06-188">Take hello following steps tooturn on hello system and restore it tooa healthy state:</span></span>

1. <span data-ttu-id="3bd06-189">如果 hello 主要機箱已開啟、 關閉電源和冷卻模組 (Pcm)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-189">If hello primary enclosure is turned on, switch off both Power and Cooling Modules (PCMs).</span></span>
2. <span data-ttu-id="3bd06-190">請等候幾分鐘，讓 hello 系統 tooshut 向下。</span><span class="sxs-lookup"><span data-stu-id="3bd06-190">Wait for a few minutes for hello system tooshut down.</span></span>
3. <span data-ttu-id="3bd06-191">開啟 hello EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-191">Turn on hello EBOD enclosure.</span></span>
4. <span data-ttu-id="3bd06-192">Hello EBOD 機箱上 」 之後，請開啟 hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-192">After hello EBOD enclosure is on, turn on hello primary enclosure.</span></span>

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a><span data-ttu-id="3bd06-193">後開啟裝置 hello 主要和 EBOD 機箱連線中斷時</span><span class="sxs-lookup"><span data-stu-id="3bd06-193">Turn on a device after hello primary and EBOD enclosure connection is lost</span></span>
<span data-ttu-id="3bd06-194">如果遺失之間 hello 待命控制器與對應 EBOD 控制器 hello hello 連接，hello 裝置會繼續 toowork。</span><span class="sxs-lookup"><span data-stu-id="3bd06-194">If hello connection is lost between hello standby controller and hello corresponding EBOD controller, hello device continues toowork.</span></span> <span data-ttu-id="3bd06-195">Hello hello 系統作用中控制器與對應 EBOD 控制器 hello 之間的連線遺失時，應該會發生容錯移轉，而 hello 裝置應該繼續 toowork 像平常一樣。</span><span class="sxs-lookup"><span data-stu-id="3bd06-195">If hello connection between hello system active controller and hello corresponding EBOD controller is lost, failover should occur and hello device should continue toowork as normal.</span></span>

<span data-ttu-id="3bd06-196">當會移除這兩個序列連接 SCSI (SAS) 纜線或切斷 EBOD 機箱 hello 與 hello 主要機箱之間的 hello 連線時，hello 裝置將會停止運作。</span><span class="sxs-lookup"><span data-stu-id="3bd06-196">When both Serial Attached SCSI (SAS) cables are removed or hello connection between hello EBOD enclosure and hello primary enclosure is severed, hello device will stop working.</span></span> <span data-ttu-id="3bd06-197">此時，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bd06-197">At this point, perform hello following steps.</span></span>

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a><span data-ttu-id="3bd06-198">tooturn hello 裝置之後，而失去連接</span><span class="sxs-lookup"><span data-stu-id="3bd06-198">tooturn on hello device after connection is lost</span></span>
1. <span data-ttu-id="3bd06-199">存取 hello hello 裝置背面。</span><span class="sxs-lookup"><span data-stu-id="3bd06-199">Access hello back of hello device.</span></span>
2. <span data-ttu-id="3bd06-200">如果 hello hello EBOD 機箱與 hello 主要機箱之間的 SAS 纜線連接已損毀，hello EBOD 機箱上所有的 SAS lane Led 都會熄滅。</span><span class="sxs-lookup"><span data-stu-id="3bd06-200">If hello SAS cable connection between hello EBOD enclosure and hello primary enclosure is broken, all SAS lane LEDs on hello EBOD enclosure will be off.</span></span>
3. <span data-ttu-id="3bd06-201">在 hello EBOD 機箱與主要機箱 hello 關閉電源和冷卻模組 (Pcm)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-201">Shut down both Power and Cooling Modules (PCMs) on hello EBOD enclosure and hello primary enclosure.</span></span>
4. <span data-ttu-id="3bd06-202">請等到所有 hello 燈號上兩個 hello 機箱的背面的 hello 都關閉。</span><span class="sxs-lookup"><span data-stu-id="3bd06-202">Wait until all hello lights on hello back of both hello enclosures turn off.</span></span>
5. <span data-ttu-id="3bd06-203">重新插入 hello SAS 纜線，並確保沒有 hello EBOD 機箱與主要機箱 hello 之間良好的連接。</span><span class="sxs-lookup"><span data-stu-id="3bd06-203">Reinsert hello SAS cables, and ensure that there is a good connection between hello EBOD enclosure and hello primary enclosure.</span></span>
6. <span data-ttu-id="3bd06-204">開啟 EBOD 機箱 hello 第一次 」 這兩個 PCM 開關 toohello 開啟 」 位置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-204">Turn on hello EBOD enclosure first by flipping both PCM switches toohello ON position.</span></span>
7. <span data-ttu-id="3bd06-205">請確認 hello EBOD 機箱上檢查 hello 綠色 LED 為 ON。</span><span class="sxs-lookup"><span data-stu-id="3bd06-205">Ensure that hello EBOD enclosure is on by checking that hello green LED is ON.</span></span>
8. <span data-ttu-id="3bd06-206">開啟 hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-206">Turn on hello primary enclosure.</span></span>
9. <span data-ttu-id="3bd06-207">請確認 hello 主要機箱上檢查 hello 控制器綠色 LED 為 「 上。</span><span class="sxs-lookup"><span data-stu-id="3bd06-207">Ensure that hello primary enclosure is on by checking that hello controller green LED is ON.</span></span>
10. <span data-ttu-id="3bd06-208">請確認該 hello hello 主要機箱與 EBOD 機箱連線良好藉由檢查該 hello SAS lane Led （每個 EBOD 控制器的四個） 都上。</span><span class="sxs-lookup"><span data-stu-id="3bd06-208">Verify that hello EBOD enclosure connection with hello primary enclosure is good by checking that hello SAS lane LEDs (four per EBOD controller) are all ON.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bd06-209">如果 hello SAS 纜線損壞或 hello hello EBOD 機箱與 hello 主要機箱之間的連線是狀況不佳，當您開啟 hello 系統時，它將會進入修復模式。</span><span class="sxs-lookup"><span data-stu-id="3bd06-209">If hello SAS cables are defective or hello connection between hello EBOD enclosure and hello primary enclosure is not good, when you turn on hello system, it will go into recovery mode.</span></span> <span data-ttu-id="3bd06-210">如果發生此情況，請 [連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md) 。</span><span class="sxs-lookup"><span data-stu-id="3bd06-210">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) if this happens.</span></span>


## <a name="turn-off-a-running-device"></a><span data-ttu-id="3bd06-211">關閉執行中的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-211">Turn off a running device</span></span>
<span data-ttu-id="3bd06-212">執行中的 StorSimple 裝置可能需要 toobe 如果它正在移動、 中斷服務，或有故障元件時，需要取代 toobe 關機。</span><span class="sxs-lookup"><span data-stu-id="3bd06-212">A running StorSimple device may need toobe shut down if it is being moved, taken out of service, or has a malfunctioning component that needs toobe replaced.</span></span> <span data-ttu-id="3bd06-213">hello 步驟會有所不同 hello StorSimple 裝置是否 8100 或 8600 模型項目。</span><span class="sxs-lookup"><span data-stu-id="3bd06-213">hello steps are different depending on whether hello StorSimple device is an 8100 or an 8600 model.</span></span> <span data-ttu-id="3bd06-214">hello 8100 具有單一主要機箱，而 hello 8600 是雙重機箱裝置，具有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-214">hello 8100 has a single primary enclosure, whereas hello 8600 is a dual-enclosure device with a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="3bd06-215">本節詳述 hello 步驟 tooshut 關閉執行中的裝置。</span><span class="sxs-lookup"><span data-stu-id="3bd06-215">This section details hello steps tooshut down a running device.</span></span>

* [<span data-ttu-id="3bd06-216">具有主要機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-216">Device with primary enclosure</span></span>](#8100a)
* [<span data-ttu-id="3bd06-217">具有 EBOD 機箱的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-217">Device with EBOD enclosure</span></span>](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a><span data-ttu-id="3bd06-218">具有主要機箱的裝置 <a name="8100a"></span><span class="sxs-lookup"><span data-stu-id="3bd06-218">Device with primary enclosure <a name="8100a"></span></span>
<span data-ttu-id="3bd06-219">tooshut hello 裝置以井然有序且受控制的方式，您可以進行透過 hello Azure 傳統入口網站或透過 hello Windows PowerShell for StorSimple。</span><span class="sxs-lookup"><span data-stu-id="3bd06-219">tooshut down hello device in an orderly and controlled manner, you can do it through hello Azure classic portal or via hello Windows PowerShell for StorSimple.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3bd06-220">不會關閉執行中的裝置使用上 hello 裝置背面的 hello hello 電源按鈕。</span><span class="sxs-lookup"><span data-stu-id="3bd06-220">Do not shut down a running device by using hello power button on hello back of hello device.</span></span>
> 
> <span data-ttu-id="3bd06-221">之前關閉 hello 裝置，請確定所有的 hello 裝置元件皆正常運作。</span><span class="sxs-lookup"><span data-stu-id="3bd06-221">Before shutting down hello device, make sure that all hello device components are healthy.</span></span> <span data-ttu-id="3bd06-222">在 hello Azure 傳統入口網站中瀏覽過**裝置** > **維護** > **硬體狀態**，並確認所有 hello 狀態元件為綠色。</span><span class="sxs-lookup"><span data-stu-id="3bd06-222">In hello Azure classic portal, navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that status of all hello components is green.</span></span> <span data-ttu-id="3bd06-223">這只適用於狀態良好的系統。</span><span class="sxs-lookup"><span data-stu-id="3bd06-223">This is true only for a healthy system.</span></span> <span data-ttu-id="3bd06-224">如果 hello 系統關機 tooreplace 的故障元件時，您會看到故障 （紅色） 或降級 （黃色） 狀態 hello hello 中的個別元件**硬體狀態**。</span><span class="sxs-lookup"><span data-stu-id="3bd06-224">If hello system is being shut down tooreplace a malfunctioning component, you will see a failed (red) or degraded (yellow) status for hello respective component in hello **Hardware Status**.</span></span>
> 
> 

<span data-ttu-id="3bd06-225">您存取 hello Windows PowerShell for StorSimple 或 hello Azure 傳統入口網站之後，請依照中的 hello 步驟[關閉 StorSimple 裝置](storsimple-manage-device-controller.md#shut-down-a-storsimple-device)。</span><span class="sxs-lookup"><span data-stu-id="3bd06-225">After you access hello Windows PowerShell for StorSimple or hello Azure classic portal, follow hello steps in [shut down a StorSimple device](storsimple-manage-device-controller.md#shut-down-a-storsimple-device).</span></span> 

### <a name="device-with-ebod-enclosure-a-name8600a"></a><span data-ttu-id="3bd06-226">具有 EBOD 機箱的裝置 <a name="8600a"></span><span class="sxs-lookup"><span data-stu-id="3bd06-226">Device with EBOD enclosure <a name="8600a"></span></span>
> [!IMPORTANT]
> <span data-ttu-id="3bd06-227">之前關閉主要機箱 hello 與 hello EBOD 機箱，請確定所有的 hello 裝置元件皆正常運作。</span><span class="sxs-lookup"><span data-stu-id="3bd06-227">Before shutting down hello primary enclosure and hello EBOD enclosure, ensure that all hello device components are healthy.</span></span> <span data-ttu-id="3bd06-228">在 hello Azure 入口網站中瀏覽過**裝置** > **監視器** > **硬體健全狀況**，並確認所有 hello 元件都均狀況良好。</span><span class="sxs-lookup"><span data-stu-id="3bd06-228">In hello Azure portal, navigate too**Devices** > **Monitor** > **Hardware health**, and verify that all hello components are healthy.</span></span>


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a><span data-ttu-id="3bd06-229">tooshut 關閉具有 EBOD 機箱執行中的裝置</span><span class="sxs-lookup"><span data-stu-id="3bd06-229">tooshut down a running device with EBOD enclosure</span></span>
1. <span data-ttu-id="3bd06-230">請遵循所列的所有 hello 步驟[關閉 StorSimple 裝置](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device)hello 主要機箱。</span><span class="sxs-lookup"><span data-stu-id="3bd06-230">Follow all hello steps listed in [shut down a StorSimple device](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) for hello primary enclosure.</span></span>
2. <span data-ttu-id="3bd06-231">之後 hello 主要機箱已關閉，關閉 hello EBOD 開關關閉電源和冷卻模組 (PCM) 的參數。</span><span class="sxs-lookup"><span data-stu-id="3bd06-231">After hello primary enclosure is shut down, shut down hello EBOD by flipping off both Power and Cooling Module (PCM) switches.</span></span>
3. <span data-ttu-id="3bd06-232">hello EBOD 的 tooverify 已關閉、 已關閉的核取所有燈號上 hello hello EBOD 機箱的背面。</span><span class="sxs-lookup"><span data-stu-id="3bd06-232">tooverify that hello EBOD has shut down, check that all lights on hello back of hello EBOD enclosure are off.</span></span>

> [!NOTE]
> <span data-ttu-id="3bd06-233">會使用的 tooconnect hello EBOD 機箱 toohello 主要機箱的 hello SAS 纜線應該後才會移除之前 hello 系統關機。</span><span class="sxs-lookup"><span data-stu-id="3bd06-233">hello SAS cables that are used tooconnect hello EBOD enclosure toohello primary enclosure should not be removed until after hello system is shut down.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bd06-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3bd06-234">Next steps</span></span>
<span data-ttu-id="3bd06-235">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) 。</span><span class="sxs-lookup"><span data-stu-id="3bd06-235">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) if you encounter problems when turning on or shutting down a StorSimple device.</span></span>

