---
title: "安裝 Microsoft Azure StorSimple 8600 裝置 | Microsoft Docs"
description: "描述如何打開包裝、掛接機架和佈線 StorSimple 8600 裝置，再部署和設定軟體。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 309ceba2d65c0745ba1acac698acb62526ab8078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a><span data-ttu-id="b44c5-103">打開包裝、掛接機架和佈線 StorSimple 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="b44c5-103">Unpack, rack-mount, and cable your StorSimple 8600 device</span></span>
## <a name="overview"></a><span data-ttu-id="b44c5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b44c5-104">Overview</span></span>
<span data-ttu-id="b44c5-105">您的 Microsoft Azure StorSimple 8600 是雙重機箱裝置，包含主要及 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-105">Your Microsoft Azure StorSimple 8600 is a dual enclosure device and consists of a primary and an EBOD enclosure.</span></span> <span data-ttu-id="b44c5-106">本教學課程說明如何在您設定 StorSimple 軟體之前，打開包裝、利用機架掛接和配接 StorSimple 8600 裝置硬體纜線。</span><span class="sxs-lookup"><span data-stu-id="b44c5-106">This tutorial explains how to unpack, rack-mount, and cable the StorSimple 8600 device hardware before you configure the StorSimple software.</span></span>

## <a name="unpack-your-storsimple-8600-device"></a><span data-ttu-id="b44c5-107">打開您的 StorSimple 8600 裝置包裝</span><span class="sxs-lookup"><span data-stu-id="b44c5-107">Unpack your StorSimple 8600 device</span></span>
<span data-ttu-id="b44c5-108">下列步驟提供如何打開 StorSimple 8600 儲存體裝置包裝的清楚、詳細指示。</span><span class="sxs-lookup"><span data-stu-id="b44c5-108">The following steps provide clear, detailed instructions on how to unpack your StorSimple 8600 storage device.</span></span> <span data-ttu-id="b44c5-109">這個裝置以兩個箱子出貨，一個用於主要機箱，另一個用於 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-109">This device is shipped in two boxes, one for the primary enclosure and another for the EBOD enclosure.</span></span> <span data-ttu-id="b44c5-110">然後這兩個箱子會放在單一的箱子中。</span><span class="sxs-lookup"><span data-stu-id="b44c5-110">These two boxes are then placed in a single box.</span></span>

### <a name="prepare-to-unpack-your-device"></a><span data-ttu-id="b44c5-111">準備打開裝置包裝</span><span class="sxs-lookup"><span data-stu-id="b44c5-111">Prepare to unpack your device</span></span>
<span data-ttu-id="b44c5-112">打開裝置包裝之前，請檢閱下列資訊。</span><span class="sxs-lookup"><span data-stu-id="b44c5-112">Before you unpack your device, review the following information.</span></span>

<span data-ttu-id="b44c5-113">![警告圖示](./media/storsimple-safety/IC740879.png)![重量圖示](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="b44c5-113">![Warning Icon](./media/storsimple-safety/IC740879.png)![heavy weight icon](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **WARNING!**</span></span>

1. <span data-ttu-id="b44c5-114">如果您手動處理它，請確定您有兩名人員可以應付裝置的重量。</span><span class="sxs-lookup"><span data-stu-id="b44c5-114">Make sure that you have two people available to manage the weight of the device if you are handling it manually.</span></span> <span data-ttu-id="b44c5-115">完全設定的機箱可以重達 32 公斤 (70 磅)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-115">A fully configured enclosure can weigh up to 32 kg (70 lbs.).</span></span>
2. <span data-ttu-id="b44c5-116">將箱子放置在平坦的表面上。</span><span class="sxs-lookup"><span data-stu-id="b44c5-116">Place the box on a flat, level surface.</span></span>

<span data-ttu-id="b44c5-117">接下來，完成下列步驟以打開裝置的包裝。</span><span class="sxs-lookup"><span data-stu-id="b44c5-117">Next, complete the following steps to unpack your device.</span></span>

#### <a name="to-unpack-your-device"></a><span data-ttu-id="b44c5-118">打開裝置包裝</span><span class="sxs-lookup"><span data-stu-id="b44c5-118">To unpack your device</span></span>
1. <span data-ttu-id="b44c5-119">檢查箱子及包裝發泡材料有無損毀、割痕、浸水，或任何其他明顯損傷。</span><span class="sxs-lookup"><span data-stu-id="b44c5-119">Inspect the box and the packaging foam for crushes, cuts, water damage, or any other obvious damage.</span></span> <span data-ttu-id="b44c5-120">如果箱子或包裝嚴重損毀，不要打開箱子。</span><span class="sxs-lookup"><span data-stu-id="b44c5-120">If the box or packaging is severely damaged, do not open the box.</span></span> <span data-ttu-id="b44c5-121">請 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以協助您評估裝置是否可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="b44c5-121">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) to help you assess whether the device is in good working order.</span></span>
2. <span data-ttu-id="b44c5-122">開啟外箱，然後取出對應主要機箱和 EBOD 機箱的兩個箱子。</span><span class="sxs-lookup"><span data-stu-id="b44c5-122">Open the outer box and then take out the two boxes corresponding to primary and EBOD enclosures.</span></span> <span data-ttu-id="b44c5-123">您現在可以拆封主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-123">You can now unpack the primary and EBOD enclosures.</span></span> <span data-ttu-id="b44c5-124">下圖顯示其中一個機箱拆封後的樣子。</span><span class="sxs-lookup"><span data-stu-id="b44c5-124">The following figure shows the unpacked view of one of the enclosures.</span></span>
   
    ![打開您的儲存體裝置包裝](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    <span data-ttu-id="b44c5-126">**儲存體裝置打開包裝的樣子**</span><span class="sxs-lookup"><span data-stu-id="b44c5-126">**Unpacked view of your storage device**</span></span>
   
   | <span data-ttu-id="b44c5-127">標籤</span><span class="sxs-lookup"><span data-stu-id="b44c5-127">Label</span></span> | <span data-ttu-id="b44c5-128">說明</span><span class="sxs-lookup"><span data-stu-id="b44c5-128">Description</span></span> |
   | --- | --- |
   |   <span data-ttu-id="b44c5-129">1</span><span class="sxs-lookup"><span data-stu-id="b44c5-129">1</span></span> |<span data-ttu-id="b44c5-130">包裝箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-130">Packing box</span></span> |
   |   <span data-ttu-id="b44c5-131">2</span><span class="sxs-lookup"><span data-stu-id="b44c5-131">2</span></span> |<span data-ttu-id="b44c5-132">SAS 纜線 (在附件和纜線匣)</span><span class="sxs-lookup"><span data-stu-id="b44c5-132">SAS cables (in accessories and cables tray)</span></span> |
   |   <span data-ttu-id="b44c5-133">3</span><span class="sxs-lookup"><span data-stu-id="b44c5-133">3</span></span> |<span data-ttu-id="b44c5-134">底層發泡材料</span><span class="sxs-lookup"><span data-stu-id="b44c5-134">Bottom foam</span></span> |
   |   <span data-ttu-id="b44c5-135">4</span><span class="sxs-lookup"><span data-stu-id="b44c5-135">4</span></span> |<span data-ttu-id="b44c5-136">裝置</span><span class="sxs-lookup"><span data-stu-id="b44c5-136">Device</span></span> |
   |   <span data-ttu-id="b44c5-137">5</span><span class="sxs-lookup"><span data-stu-id="b44c5-137">5</span></span> |<span data-ttu-id="b44c5-138">頂層發泡材料</span><span class="sxs-lookup"><span data-stu-id="b44c5-138">Top foam</span></span> |
   |   <span data-ttu-id="b44c5-139">6</span><span class="sxs-lookup"><span data-stu-id="b44c5-139">6</span></span> |<span data-ttu-id="b44c5-140">附件箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-140">Accessory box</span></span> |
3. <span data-ttu-id="b44c5-141">打開兩個箱子的包裝之後，請確定您有：</span><span class="sxs-lookup"><span data-stu-id="b44c5-141">After unpacking the two boxes, make sure that you have:</span></span>
   
   * <span data-ttu-id="b44c5-142">1 個主要機箱 (主要機箱與 EBOD 機箱是在兩個不同的箱子中)</span><span class="sxs-lookup"><span data-stu-id="b44c5-142">1 primary enclosure (the primary enclosure and EBOD enclosure are in two separate boxes)</span></span>
   * <span data-ttu-id="b44c5-143">1 個 EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-143">1 EBOD enclosure</span></span>
   * <span data-ttu-id="b44c5-144">4 條電源線，每個箱子各 2 條</span><span class="sxs-lookup"><span data-stu-id="b44c5-144">4 power cords, 2 in each box</span></span>
   * <span data-ttu-id="b44c5-145">2 條 SAS 纜線 (連接主要機箱與 EBOD 機箱)</span><span class="sxs-lookup"><span data-stu-id="b44c5-145">2 SAS cables (to connect the primary enclosure to EBOD enclosure)</span></span>
   * <span data-ttu-id="b44c5-146">1 條轉接乙太網路纜線</span><span class="sxs-lookup"><span data-stu-id="b44c5-146">1 crossover Ethernet cable</span></span>
   * <span data-ttu-id="b44c5-147">2 條序列主控台纜線</span><span class="sxs-lookup"><span data-stu-id="b44c5-147">2 serial console cables</span></span>
   * <span data-ttu-id="b44c5-148">1 個用於序列存取的序列-USB 轉換器</span><span class="sxs-lookup"><span data-stu-id="b44c5-148">1 serial-USB converter for serial access</span></span>
   * <span data-ttu-id="b44c5-149">4 個 QSFP-to-SFP+ 配接器以用於 10 GbE 網路介面</span><span class="sxs-lookup"><span data-stu-id="b44c5-149">4 QSFP-to-SFP+ adapters for use with 10 GbE network interfaces</span></span>
   * <span data-ttu-id="b44c5-150">2 個機架掛接套件 (4 個側軌掛接硬體，主要機箱與 EBOD 機箱各 2 個)，每個箱子中各 1 個</span><span class="sxs-lookup"><span data-stu-id="b44c5-150">2 rack mount kits (4 side rails with mounting hardware, 2 each for the primary enclosure and EBOD enclosure), 1 in each box</span></span>
   * <span data-ttu-id="b44c5-151">開始使用文件</span><span class="sxs-lookup"><span data-stu-id="b44c5-151">Getting started documentation</span></span>
     
     <span data-ttu-id="b44c5-152">如果您未收到任何上述項目，請[連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-152">If you did not receive any of the items listed above, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>  

<span data-ttu-id="b44c5-153">下一步是利用機架掛接裝置。</span><span class="sxs-lookup"><span data-stu-id="b44c5-153">The next step is to rack-mount your device.</span></span>

## <a name="rack-mount-your-storsimple-8600-device"></a><span data-ttu-id="b44c5-154">機架掛接您的 StorSimple 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="b44c5-154">Rack-mount your StorSimple 8600 device</span></span>
<span data-ttu-id="b44c5-155">遵循下列步驟，以具有前後端柱子的標準 19 英吋機架安裝 StorSimple 8600 儲存體裝置。</span><span class="sxs-lookup"><span data-stu-id="b44c5-155">Follow the next steps to install your StorSimple 8600 storage device in a standard 19-inch rack with front and rear posts.</span></span> <span data-ttu-id="b44c5-156">此裝置有兩個機箱：主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-156">This device comes with two enclosures: a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="b44c5-157">兩個機箱都需要機架掛接。</span><span class="sxs-lookup"><span data-stu-id="b44c5-157">Both of these need to be rack-mounted.</span></span>

<span data-ttu-id="b44c5-158">安裝包含多個步驟，會在下列程序中討論每個步驟。</span><span class="sxs-lookup"><span data-stu-id="b44c5-158">The installation consists of multiple steps, each of which is discussed in the following procedures.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b44c5-159">StorSimple 裝置需要機架掛接才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="b44c5-159">StorSimple devices must be rack-mounted for proper operation.</span></span>
> 
> 

### <a name="site-preparation"></a><span data-ttu-id="b44c5-160">場地準備</span><span class="sxs-lookup"><span data-stu-id="b44c5-160">Site preparation</span></span>
<span data-ttu-id="b44c5-161">機箱必須安裝在具有前後端柱子的標準 19 英吋機架上。</span><span class="sxs-lookup"><span data-stu-id="b44c5-161">The enclosures must be installed in a standard 19-inch rack that has both front and rear posts.</span></span> <span data-ttu-id="b44c5-162">使用下列程序來準備機架安裝。</span><span class="sxs-lookup"><span data-stu-id="b44c5-162">Use the following procedure to prepare for rack installation.</span></span>

#### <a name="to-prepare-the-site-for-rack-installation"></a><span data-ttu-id="b44c5-163">準備場地進行機架安裝</span><span class="sxs-lookup"><span data-stu-id="b44c5-163">To prepare the site for rack installation</span></span>
1. <span data-ttu-id="b44c5-164">請確定主要和 EBOD 機箱安全地放在平坦、穩定的工作介面 (或類似)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-164">Make sure that the primary and EBOD enclosures are resting safely on a flat, stable, and level work surface (or similar).</span></span>
2. <span data-ttu-id="b44c5-165">請確認您想要安裝的場地具有獨立來源的標準 AC 電源，或是具有不斷電供應系統 (UPS) 的機架電源分配單元 (PDU)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-165">Verify that the site where you intend to set up has standard AC power from an independent source or a rack Power Distribution Unit (PDU) with an uninterruptible power supply (UPS).</span></span>
3. <span data-ttu-id="b44c5-166">請確定您要掛接機箱的機架上有一個 4U (2 X 2U) 插槽可用。</span><span class="sxs-lookup"><span data-stu-id="b44c5-166">Make sure that one 4U (2 X 2U) slot is available on the rack in which you intend to mount the enclosures.</span></span>

<span data-ttu-id="b44c5-167">![警告圖示](./media/storsimple-safety/IC740879.png)![重量圖示](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **警告！**</span><span class="sxs-lookup"><span data-stu-id="b44c5-167">![Warning Icon](./media/storsimple-safety/IC740879.png)![heavy weight icon](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **WARNING!**</span></span>

 <span data-ttu-id="b44c5-168">如果您手動處理裝置安裝，請確定您有兩名人員可以應付裝置的重量。</span><span class="sxs-lookup"><span data-stu-id="b44c5-168">Make sure that you have two people available to manage the weight if you are handling the device setup manually.</span></span> <span data-ttu-id="b44c5-169">完全設定的機箱可以重達 32 公斤 (70 磅)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-169">A fully configured enclosure can weigh up to 32 kg (70 lbs.).</span></span>

### <a name="rack-prerequisites"></a><span data-ttu-id="b44c5-170">機架必要條件</span><span class="sxs-lookup"><span data-stu-id="b44c5-170">Rack prerequisites</span></span>
<span data-ttu-id="b44c5-171">機箱是針對安裝在具有下列項目的標準 19 英吋機櫃而設計的：</span><span class="sxs-lookup"><span data-stu-id="b44c5-171">The enclosures are designed for installation in a standard 19-inch rack cabinet with:</span></span>

* <span data-ttu-id="b44c5-172">從機架柱到柱子最小深度為 27.84 英吋</span><span class="sxs-lookup"><span data-stu-id="b44c5-172">Minimum depth of 27.84 inches from rack post to post</span></span>
* <span data-ttu-id="b44c5-173">裝置的最大重量為 32 公斤</span><span class="sxs-lookup"><span data-stu-id="b44c5-173">Maximum weight of 32 kg for the device</span></span>
* <span data-ttu-id="b44c5-174">最大背部壓力為 5 Pascal (0.5 mm 水位表)</span><span class="sxs-lookup"><span data-stu-id="b44c5-174">Maximum back pressure of 5 Pascal (0.5 mm water gauge)</span></span>

### <a name="rack-mounting-rail-kit"></a><span data-ttu-id="b44c5-175">機架掛接滑軌套件</span><span class="sxs-lookup"><span data-stu-id="b44c5-175">Rack-mounting rail kit</span></span>
<span data-ttu-id="b44c5-176">提供一組掛接滑軌以用於 19 英吋機櫃。</span><span class="sxs-lookup"><span data-stu-id="b44c5-176">A set of mounting rails will be provided for use with the 19-inch rack cabinet.</span></span> <span data-ttu-id="b44c5-177">滑軌已經過測試可以處理最大機箱重量。</span><span class="sxs-lookup"><span data-stu-id="b44c5-177">The rails have been tested to handle the maximum enclosure weight.</span></span> <span data-ttu-id="b44c5-178">這些滑軌也可以進行多個機箱的安裝，而不會損失機櫃內的空間。</span><span class="sxs-lookup"><span data-stu-id="b44c5-178">These rails will also allow installation of multiple enclosures without loss of space within the rack.</span></span> <span data-ttu-id="b44c5-179">先安裝 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-179">Install the EBOD enclosure first.</span></span>

#### <a name="to-install-the-ebod-enclosure-on-the-rails"></a><span data-ttu-id="b44c5-180">在滑軌上安裝 EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-180">To install the EBOD enclosure on the rails</span></span>
1. <span data-ttu-id="b44c5-181">只有在內部滑軌未安裝在您的裝置上時才執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="b44c5-181">Perform this step only if inner rails are not installed on your device.</span></span> <span data-ttu-id="b44c5-182">通常，內部滑軌會在工廠安裝。</span><span class="sxs-lookup"><span data-stu-id="b44c5-182">Typically, the inner rails are installed at the factory.</span></span> <span data-ttu-id="b44c5-183">如果滑軌沒有安裝的話，則在機箱底座側邊安裝左邊和右邊滑軌。</span><span class="sxs-lookup"><span data-stu-id="b44c5-183">If rails are not installed, then install the left-rail and right-rail slides to the sides of the enclosure chassis.</span></span> <span data-ttu-id="b44c5-184">它們是在每一邊使用六個公制螺絲來連接。</span><span class="sxs-lookup"><span data-stu-id="b44c5-184">They attach using six metric screws on each side.</span></span> <span data-ttu-id="b44c5-185">為了協助辨識方向，滑軌標示為 [LH – Front] \(左邊 – 前) 和 [RH – Front] \(右邊 – 前)，接至機箱後端的尾端有錐型結尾。</span><span class="sxs-lookup"><span data-stu-id="b44c5-185">To help with orientation, the rail slides are marked **LH – Front** and **RH – Front**, and the end that is affixed towards the rear of the enclosure has a tapered end.</span></span>
   
    ![將滑軌連接至機箱底座](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    <span data-ttu-id="b44c5-187">**將滑軌連接至機箱側邊**</span><span class="sxs-lookup"><span data-stu-id="b44c5-187">**Attaching rail slides to the sides of the enclosure**</span></span>
   
   | <span data-ttu-id="b44c5-188">標籤</span><span class="sxs-lookup"><span data-stu-id="b44c5-188">Label</span></span> | <span data-ttu-id="b44c5-189">說明</span><span class="sxs-lookup"><span data-stu-id="b44c5-189">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="b44c5-190">1</span><span class="sxs-lookup"><span data-stu-id="b44c5-190">1</span></span> |<span data-ttu-id="b44c5-191">M 3x4 圓頭螺釘</span><span class="sxs-lookup"><span data-stu-id="b44c5-191">M 3x4 button-head screws</span></span> |
   |  <span data-ttu-id="b44c5-192">2</span><span class="sxs-lookup"><span data-stu-id="b44c5-192">2</span></span> |<span data-ttu-id="b44c5-193">底座滑軌</span><span class="sxs-lookup"><span data-stu-id="b44c5-193">Chassis slides</span></span> |
2. <span data-ttu-id="b44c5-194">將左邊滑軌和右邊滑軌組件連接至機櫃垂直面。</span><span class="sxs-lookup"><span data-stu-id="b44c5-194">Attach the left rail and right rail assemblies to the rack cabinet vertical members.</span></span> <span data-ttu-id="b44c5-195">托架會標示 [LH] \(左邊)，[RH] \(右邊) 和 [This side up] \(此面向上)，引導您正確的方向。</span><span class="sxs-lookup"><span data-stu-id="b44c5-195">The brackets are marked **LH**, **RH**, and **This side up** to guide you through correct orientation.</span></span>
3. <span data-ttu-id="b44c5-196">找出滑軌組件前後方的滑軌插梢。</span><span class="sxs-lookup"><span data-stu-id="b44c5-196">Locate the rail pins at the front and rear of the rail assembly.</span></span> <span data-ttu-id="b44c5-197">延伸滑軌以適合機架柱，並且將插梢插入前後端機架柱垂直面的孔洞。</span><span class="sxs-lookup"><span data-stu-id="b44c5-197">Extend the rail to fit between the rack posts and insert the pins into the front and rear-rack post vertical member holes.</span></span> <span data-ttu-id="b44c5-198">請確定滑軌組件是水平的。</span><span class="sxs-lookup"><span data-stu-id="b44c5-198">Be sure that the rail assembly is level.</span></span>
4. <span data-ttu-id="b44c5-199">使用兩個提供的公制螺絲將滑軌組件鎖固至機架垂直面。</span><span class="sxs-lookup"><span data-stu-id="b44c5-199">Secure the rail assembly to the rack vertical members by using two of the metric screws provided.</span></span> <span data-ttu-id="b44c5-200">在前端和後端各使用一個螺絲。</span><span class="sxs-lookup"><span data-stu-id="b44c5-200">Use one screw on the front and one on the rear.</span></span>
5. <span data-ttu-id="b44c5-201">對其他滑軌組件重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="b44c5-201">Repeat these steps for the other rail assembly.</span></span>
   
     ![將滑軌連接至機櫃](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    <span data-ttu-id="b44c5-203">**將滑軌組件連接至機架**</span><span class="sxs-lookup"><span data-stu-id="b44c5-203">**Attaching rail assemblies to the rack**</span></span>
   
   | <span data-ttu-id="b44c5-204">標籤</span><span class="sxs-lookup"><span data-stu-id="b44c5-204">Label</span></span> | <span data-ttu-id="b44c5-205">說明</span><span class="sxs-lookup"><span data-stu-id="b44c5-205">Description</span></span> |
   | --- | --- |
   |   <span data-ttu-id="b44c5-206">1</span><span class="sxs-lookup"><span data-stu-id="b44c5-206">1</span></span> |<span data-ttu-id="b44c5-207">固定螺絲</span><span class="sxs-lookup"><span data-stu-id="b44c5-207">Clamping screw</span></span> |
   |   <span data-ttu-id="b44c5-208">2</span><span class="sxs-lookup"><span data-stu-id="b44c5-208">2</span></span> |<span data-ttu-id="b44c5-209">方孔前端機架柱螺絲</span><span class="sxs-lookup"><span data-stu-id="b44c5-209">Square-hole front rack post screw</span></span> |
   |   <span data-ttu-id="b44c5-210">3</span><span class="sxs-lookup"><span data-stu-id="b44c5-210">3</span></span> |<span data-ttu-id="b44c5-211">左邊前端滑軌位置插梢</span><span class="sxs-lookup"><span data-stu-id="b44c5-211">Left front rail location pins</span></span> |
   |   <span data-ttu-id="b44c5-212">4</span><span class="sxs-lookup"><span data-stu-id="b44c5-212">4</span></span> |<span data-ttu-id="b44c5-213">固定螺絲</span><span class="sxs-lookup"><span data-stu-id="b44c5-213">Clamping screw</span></span> |
   |   <span data-ttu-id="b44c5-214">5</span><span class="sxs-lookup"><span data-stu-id="b44c5-214">5</span></span> |<span data-ttu-id="b44c5-215">左邊後端滑軌位置插梢</span><span class="sxs-lookup"><span data-stu-id="b44c5-215">Left rear rail location pins</span></span> |

### <a name="mounting-the-ebod-enclosure-in-the-rack"></a><span data-ttu-id="b44c5-216">在機架中掛接 EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-216">Mounting the EBOD enclosure in the rack</span></span>
<span data-ttu-id="b44c5-217">使用剛才安裝的機架滑軌，執行下列步驟以在機架中掛接 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-217">Using the rack rails that were just installed, perform the following steps to mount the EBOD enclosure in the rack.</span></span>

#### <a name="to-mount-the-ebod-enclosure"></a><span data-ttu-id="b44c5-218">掛接 EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-218">To mount the EBOD enclosure</span></span>
1. <span data-ttu-id="b44c5-219">使用輔助工具，將機箱抬起並且對齊機架滑軌。</span><span class="sxs-lookup"><span data-stu-id="b44c5-219">With an assistant, lift the enclosure and align it with the rack rails.</span></span>
2. <span data-ttu-id="b44c5-220">仔細地將機箱插入滑軌，然後將機箱完全推入至機櫃。</span><span class="sxs-lookup"><span data-stu-id="b44c5-220">Carefully insert the enclosure into the rails, and then push it completely into the rack cabinet.</span></span>
   
    ![在機架中插入裝置](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    <span data-ttu-id="b44c5-222">**在機架中掛接機箱**</span><span class="sxs-lookup"><span data-stu-id="b44c5-222">**Mounting the enclosure in the rack**</span></span>
3. <span data-ttu-id="b44c5-223">鬆開蓋子以移除左右前端輪緣蓋。</span><span class="sxs-lookup"><span data-stu-id="b44c5-223">Remove the left and right front flange caps by pulling the caps free.</span></span> <span data-ttu-id="b44c5-224">輪緣蓋只是卡在輪緣上。</span><span class="sxs-lookup"><span data-stu-id="b44c5-224">The flange caps simply snap onto the flanges.</span></span>
4. <span data-ttu-id="b44c5-225">藉由在每個輪緣、左側和右側，安裝一個提供的十字螺絲，在機架中鎖固機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-225">Secure the enclosure into the rack by installing one provided Phillips-head screw through each flange, left and right.</span></span>
5. <span data-ttu-id="b44c5-226">安裝輪緣蓋，方法是將其推入定位並且扣住。</span><span class="sxs-lookup"><span data-stu-id="b44c5-226">Install the flange caps by pressing them into position and snapping them into place.</span></span>
   
     ![安裝輪緣蓋](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    <span data-ttu-id="b44c5-228">**安裝輪緣蓋**</span><span class="sxs-lookup"><span data-stu-id="b44c5-228">**Installing the flange caps**</span></span>
   
   | <span data-ttu-id="b44c5-229">標籤</span><span class="sxs-lookup"><span data-stu-id="b44c5-229">Label</span></span> | <span data-ttu-id="b44c5-230">說明</span><span class="sxs-lookup"><span data-stu-id="b44c5-230">Description</span></span> |
   | --- | --- |
   |   <span data-ttu-id="b44c5-231">1</span><span class="sxs-lookup"><span data-stu-id="b44c5-231">1</span></span> |<span data-ttu-id="b44c5-232">機箱鎖固螺絲</span><span class="sxs-lookup"><span data-stu-id="b44c5-232">Enclosure fastening screw</span></span> |

### <a name="mounting-the-primary-enclosure-in-the-rack"></a><span data-ttu-id="b44c5-233">在機架中掛接主要機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-233">Mounting the primary enclosure in the rack</span></span>
<span data-ttu-id="b44c5-234">完成掛接 EBOD 機箱之後，您必須遵循相同步驟以掛接主要機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-234">After you have finished mounting the EBOD enclosure, you will need to mount the primary enclosure following the same steps.</span></span>

> [!NOTE]
> * <span data-ttu-id="b44c5-235">主要機箱與 EBOD 機箱之間的機架中可能會有一些空的插槽。</span><span class="sxs-lookup"><span data-stu-id="b44c5-235">It is possible to have a few empty slots in the rack between the primary enclosure and the EBOD enclosure.</span></span>
> * <span data-ttu-id="b44c5-236">使用提供的 2m SAS 纜線以連接主要機箱與 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-236">Use the provided 2m SAS cable to connect the primary enclosure to the EBOD enclosure.</span></span>
> * <span data-ttu-id="b44c5-237">EBOD 單元的前端單元相對位置沒有限制。</span><span class="sxs-lookup"><span data-stu-id="b44c5-237">There are no constraints on the relative placement of the head unit to the EBOD unit.</span></span> <span data-ttu-id="b44c5-238">因此，主要機箱可以放在最上層插槽中，而 EBOD 機箱可以放在下方，或者反之亦然。</span><span class="sxs-lookup"><span data-stu-id="b44c5-238">Therefore, the primary enclosure can be placed in the top slot and the EBOD enclosure below — or vice versa.</span></span>
> 
> 

<span data-ttu-id="b44c5-239">下一個步驟是針對裝置的電源、網路和序列存取進行佈線。</span><span class="sxs-lookup"><span data-stu-id="b44c5-239">The next step is to cable your device for power, network, and serial access.</span></span>

## <a name="cable-your-storsimple-8600-device"></a><span data-ttu-id="b44c5-240">佈線您的 StorSimple 8600 裝置</span><span class="sxs-lookup"><span data-stu-id="b44c5-240">Cable your StorSimple 8600 device</span></span>
<span data-ttu-id="b44c5-241">下列程序說明如何針對 StorSimple 8600 裝置的電源、網路和序列連線進行佈線。</span><span class="sxs-lookup"><span data-stu-id="b44c5-241">The following procedures explain how to cable your StorSimple 8600 device for power, network, and serial connections.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b44c5-242">必要條件</span><span class="sxs-lookup"><span data-stu-id="b44c5-242">Prerequisites</span></span>
<span data-ttu-id="b44c5-243">開始您的裝置佈線之前，您需要：</span><span class="sxs-lookup"><span data-stu-id="b44c5-243">Before you begin to cable your device, you will need:</span></span>

* <span data-ttu-id="b44c5-244">完全打開您的主要機箱與 EBOD 機箱的包裝</span><span class="sxs-lookup"><span data-stu-id="b44c5-244">Your primary enclosure and the EBOD enclosure, completely unpacked</span></span>
* <span data-ttu-id="b44c5-245">隨附於您的裝置的 4 條電源線 (主要及 EBOD 機箱各 2 條)</span><span class="sxs-lookup"><span data-stu-id="b44c5-245">4 power cables (2 each for the primary and the EBOD enclosure) that came with your device</span></span>
* <span data-ttu-id="b44c5-246">裝置隨附的 2 條 SAS 纜線以連接主要機箱與 EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-246">2 SAS cables supplied with the device to connect the EBOD enclosure to the primary enclosure</span></span>
* <span data-ttu-id="b44c5-247">可以存取 2 個電源分配單元 (PDU) (建議)</span><span class="sxs-lookup"><span data-stu-id="b44c5-247">Access to 2 Power Distribution Units (PDUs) (recommended)</span></span>
* <span data-ttu-id="b44c5-248">網路纜線</span><span class="sxs-lookup"><span data-stu-id="b44c5-248">Network cables</span></span>
* <span data-ttu-id="b44c5-249">提供的序列纜線</span><span class="sxs-lookup"><span data-stu-id="b44c5-249">Provided serial cables</span></span>
* <span data-ttu-id="b44c5-250">序列 USB 轉換器，且您的電腦上已安裝適當驅動程式 (如果需要)</span><span class="sxs-lookup"><span data-stu-id="b44c5-250">Serial-USB converter with the appropriate driver installed on your PC (if needed)</span></span>
* <span data-ttu-id="b44c5-251">提供 4 個 QSFP-to-SFP+ 配接器以用於 10 GbE 網路介面</span><span class="sxs-lookup"><span data-stu-id="b44c5-251">Provided 4 QSFP-to-SFP+ adapters for use with 10 GbE network interfaces</span></span>
* [<span data-ttu-id="b44c5-252">10 GbE 網路介面在 StorSimple 裝置上支援的硬體</span><span class="sxs-lookup"><span data-stu-id="b44c5-252">Supported hardware for the 10 GbE network interfaces on your StorSimple device</span></span>](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a><span data-ttu-id="b44c5-253">SAS 及電源佈線</span><span class="sxs-lookup"><span data-stu-id="b44c5-253">SAS and Power cabling</span></span>
<span data-ttu-id="b44c5-254">您的裝置同時有主要機箱和 EBOD 機箱。</span><span class="sxs-lookup"><span data-stu-id="b44c5-254">Your device has both a primary enclosure and an EBOD enclosure.</span></span> <span data-ttu-id="b44c5-255">這需要使用纜線將單元連接在一起，以取得序列連接 SCSI (SAS) 連線與電源。</span><span class="sxs-lookup"><span data-stu-id="b44c5-255">This requires the units to be cabled together for Serial Attached SCSI (SAS) connectivity and power.</span></span>

<span data-ttu-id="b44c5-256">第一次設定此裝置時，請先執行 SAS 佈線步驟，然後再完成電源佈線步驟。</span><span class="sxs-lookup"><span data-stu-id="b44c5-256">When setting up this device for the first time, perform the steps for SAS cabling first and then complete the steps for power cabling.</span></span>

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a><span data-ttu-id="b44c5-257">網路佈線</span><span class="sxs-lookup"><span data-stu-id="b44c5-257">Network cabling</span></span>
<span data-ttu-id="b44c5-258">您的裝置是作用中待命組態：在任何指定時間，一個控制器模組為作用中，且在其他控制器模組待命時處理所有磁碟和網路作業。</span><span class="sxs-lookup"><span data-stu-id="b44c5-258">Your device is in an active-standby configuration: at any given time, one controller module is active and processing all disk and network operations while the other controller module is on standby.</span></span> <span data-ttu-id="b44c5-259">如果控制器失敗，則待命控制器會立即啟動，並且繼續所有磁碟和網路作業。</span><span class="sxs-lookup"><span data-stu-id="b44c5-259">If a controller failure occurs, the standby controller immediately activates and continues all the disk and networking operations.</span></span>

<span data-ttu-id="b44c5-260">若要支援此備援控制器容錯移轉，您需要如下列步驟所示佈線您的裝置網路。</span><span class="sxs-lookup"><span data-stu-id="b44c5-260">To support this redundant controller failover, you need to cable your device network as shown in the following steps.</span></span>

#### <a name="to-cable-for-network-connection"></a><span data-ttu-id="b44c5-261">佈線網路連線</span><span class="sxs-lookup"><span data-stu-id="b44c5-261">To cable for network connection</span></span>
1. <span data-ttu-id="b44c5-262">您的裝置在每個控制器上有六個網路介面：四個 1 Gbps 和兩個 10 Gbps 乙太網路連接埠。</span><span class="sxs-lookup"><span data-stu-id="b44c5-262">Your device has six network interfaces on each controller: four 1 Gbps and two 10 Gbps Ethernet ports.</span></span> <span data-ttu-id="b44c5-263">請參閱下圖以識別裝置後擋板上的各個資料連接埠。</span><span class="sxs-lookup"><span data-stu-id="b44c5-263">Refer to the following illustration to identify the data ports on the backplane of your device.</span></span>
   
     ![8600 裝置的後擋板](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    <span data-ttu-id="b44c5-265">**裝置後方的資料連接埠**</span><span class="sxs-lookup"><span data-stu-id="b44c5-265">**Back of your device showing the data ports**</span></span>
   
   | <span data-ttu-id="b44c5-266">標籤</span><span class="sxs-lookup"><span data-stu-id="b44c5-266">Label</span></span> | <span data-ttu-id="b44c5-267">說明</span><span class="sxs-lookup"><span data-stu-id="b44c5-267">Description</span></span> |
   | --- | --- |
   |   <span data-ttu-id="b44c5-268">0,1,4,5</span><span class="sxs-lookup"><span data-stu-id="b44c5-268">0,1,4,5</span></span> |<span data-ttu-id="b44c5-269">1 GbE 網路介面</span><span class="sxs-lookup"><span data-stu-id="b44c5-269">1 GbE network interfaces</span></span> |
   |   <span data-ttu-id="b44c5-270">2,3</span><span class="sxs-lookup"><span data-stu-id="b44c5-270">2,3</span></span> |<span data-ttu-id="b44c5-271">10 GbE 網路介面</span><span class="sxs-lookup"><span data-stu-id="b44c5-271">10 GbE network interfaces</span></span> |
   |   <span data-ttu-id="b44c5-272">6</span><span class="sxs-lookup"><span data-stu-id="b44c5-272">6</span></span> |<span data-ttu-id="b44c5-273">序列連接埠</span><span class="sxs-lookup"><span data-stu-id="b44c5-273">Serial ports</span></span> |
2. <span data-ttu-id="b44c5-274">請參閱下圖的網路佈線。</span><span class="sxs-lookup"><span data-stu-id="b44c5-274">See the following diagram for network cabling.</span></span> <span data-ttu-id="b44c5-275">(最小的網路組態會以藍色實線顯示。</span><span class="sxs-lookup"><span data-stu-id="b44c5-275">(The minimum network configuration is shown by solid blue lines.</span></span> <span data-ttu-id="b44c5-276">對於高可用性和效能，需要的其他組態會以虛線顯示。)</span><span class="sxs-lookup"><span data-stu-id="b44c5-276">For high availability and performance, additional configuration required is shown by dotted lines.)</span></span>

![為您的 4U 裝置進行網路佈線](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

<span data-ttu-id="b44c5-278">**您裝置的網路纜線**</span><span class="sxs-lookup"><span data-stu-id="b44c5-278">**Network cabling for your device**</span></span>

| <span data-ttu-id="b44c5-279">標籤</span><span class="sxs-lookup"><span data-stu-id="b44c5-279">Label</span></span> | <span data-ttu-id="b44c5-280">說明</span><span class="sxs-lookup"><span data-stu-id="b44c5-280">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b44c5-281">A</span><span class="sxs-lookup"><span data-stu-id="b44c5-281">A</span></span> |<span data-ttu-id="b44c5-282">具有網際網路存取的 LAN</span><span class="sxs-lookup"><span data-stu-id="b44c5-282">LAN with Internet access</span></span> |
| <span data-ttu-id="b44c5-283">B</span><span class="sxs-lookup"><span data-stu-id="b44c5-283">B</span></span> |<span data-ttu-id="b44c5-284">控制器 0</span><span class="sxs-lookup"><span data-stu-id="b44c5-284">Controller 0</span></span> |
| <span data-ttu-id="b44c5-285">C</span><span class="sxs-lookup"><span data-stu-id="b44c5-285">C</span></span> |<span data-ttu-id="b44c5-286">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b44c5-286">PCM 0</span></span> |
| <span data-ttu-id="b44c5-287">D</span><span class="sxs-lookup"><span data-stu-id="b44c5-287">D</span></span> |<span data-ttu-id="b44c5-288">控制器 1</span><span class="sxs-lookup"><span data-stu-id="b44c5-288">Controller 1</span></span> |
| <span data-ttu-id="b44c5-289">E</span><span class="sxs-lookup"><span data-stu-id="b44c5-289">E</span></span> |<span data-ttu-id="b44c5-290">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b44c5-290">PCM 1</span></span> |
| <span data-ttu-id="b44c5-291">F</span><span class="sxs-lookup"><span data-stu-id="b44c5-291">F</span></span> |<span data-ttu-id="b44c5-292">EBOD 控制器 0</span><span class="sxs-lookup"><span data-stu-id="b44c5-292">EBOD controller 0</span></span> |
| <span data-ttu-id="b44c5-293">G</span><span class="sxs-lookup"><span data-stu-id="b44c5-293">G</span></span> |<span data-ttu-id="b44c5-294">EBOD 控制器 1</span><span class="sxs-lookup"><span data-stu-id="b44c5-294">EBOD controller 1</span></span> |
| <span data-ttu-id="b44c5-295">H,I</span><span class="sxs-lookup"><span data-stu-id="b44c5-295">H,I</span></span> |<span data-ttu-id="b44c5-296">主機 (例如，檔案伺服器)</span><span class="sxs-lookup"><span data-stu-id="b44c5-296">Hosts (for example, file servers)</span></span> |
| <span data-ttu-id="b44c5-297">0-5</span><span class="sxs-lookup"><span data-stu-id="b44c5-297">0-5</span></span> |<span data-ttu-id="b44c5-298">網路介面</span><span class="sxs-lookup"><span data-stu-id="b44c5-298">Network interfaces</span></span> |
| <span data-ttu-id="b44c5-299">6</span><span class="sxs-lookup"><span data-stu-id="b44c5-299">6</span></span> |<span data-ttu-id="b44c5-300">主要機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-300">Primary enclosure</span></span> |
| <span data-ttu-id="b44c5-301">7</span><span class="sxs-lookup"><span data-stu-id="b44c5-301">7</span></span> |<span data-ttu-id="b44c5-302">EBOD 機箱</span><span class="sxs-lookup"><span data-stu-id="b44c5-302">EBOD enclosure</span></span> |

<span data-ttu-id="b44c5-303">當連接裝置纜線時，最低設定需要：</span><span class="sxs-lookup"><span data-stu-id="b44c5-303">When cabling the device, the minimum configuration requires:</span></span>

* <span data-ttu-id="b44c5-304">各個控制器上至少已連接兩個網路介面，一個用於雲端存取，一個用於 iSCSI。</span><span class="sxs-lookup"><span data-stu-id="b44c5-304">At least two network interfaces connected on each controller with one for cloud access and one for iSCSI.</span></span> <span data-ttu-id="b44c5-305">DATA 0 連接埠會自動啟用並透過裝置的序列主控台設定。</span><span class="sxs-lookup"><span data-stu-id="b44c5-305">The DATA 0 port is automatically enabled and configured via the serial console of the device.</span></span> <span data-ttu-id="b44c5-306">除了 DATA 0，另一個資料連接埠也需要透過 Azure 傳統入口網站來設定。</span><span class="sxs-lookup"><span data-stu-id="b44c5-306">Apart from DATA 0, another data port also needs to be configured through the Azure classic portal.</span></span> <span data-ttu-id="b44c5-307">在此情況下，請將 DATA 0 連接埠連接到主要區域網路 (具有網際網路存取的網路)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-307">In this case, connect DATA 0 port to the primary LAN (network with Internet access).</span></span> <span data-ttu-id="b44c5-308">其他資料連接埠可以連線到網路的 SAN/iSCSI LAN (VLAN) 區段，視預期的角色而定。</span><span class="sxs-lookup"><span data-stu-id="b44c5-308">The other data ports can be connected to SAN/iSCSI LAN (VLAN) segment of the network, depending on the intended role.</span></span>
* <span data-ttu-id="b44c5-309">各個控制器上的相同介面已連接到相同的網路以確保可用性 (如果發生控制器容錯移轉)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-309">Identical interfaces on each controller connected to the same network to ensure availability if a controller failover occurs.</span></span> <span data-ttu-id="b44c5-310">例如，如果您選擇對於其中一個控制器連接 DATA 0 和 DATA 3，您需要在其他控制器上連接對應的 DATA 0 和 DATA 3。</span><span class="sxs-lookup"><span data-stu-id="b44c5-310">For instance, if you choose to connect DATA 0 and DATA 3 for one of the controllers, you need to connect the corresponding DATA 0 and DATA 3 on the other controller.</span></span>

<span data-ttu-id="b44c5-311">針對高可用性和效能，請記住：</span><span class="sxs-lookup"><span data-stu-id="b44c5-311">Keep in mind for high availability and performance:</span></span>

* <span data-ttu-id="b44c5-312">可能的話，請在各個控制器上設定一組用於雲端存取 (1 GbE)，和另一組用於 iSCSI (建議 10 GbE) 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="b44c5-312">When possible, configure a pair of network interface for cloud access (1 GbE) and another pair for iSCSI (10 GbE recommended) on each controller.</span></span>
* <span data-ttu-id="b44c5-313">可能的話，請將各個控制器的網路介面連接到兩個不同的交換器，以確保交換器發生錯誤時的可用性。</span><span class="sxs-lookup"><span data-stu-id="b44c5-313">When possible, connect network interfaces from each controller to two different switches to ensure availability against a switch failure.</span></span> <span data-ttu-id="b44c5-314">下圖說明兩個從各個控制器連接到兩個不同交換器的 10 GbE 網路介面 (DATA 2 和 DATA 3)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-314">The figure illustrates the two 10 GbE network interfaces, DATA 2 and DATA 3, from each controller connected to two different switches.</span></span> <span data-ttu-id="b44c5-315">如需詳細資訊，請參閱 **StorSimple 裝置的高可用性需求** 下的 [網路介面](storsimple-system-requirements.md#high-availability-requirements-for-storsimple)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-315">For more information, refer to the **Network interfaces** under the [High availability requirements for your StorSimple device](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).</span></span>

> [!NOTE]
> <span data-ttu-id="b44c5-316">如果搭配使用 SFP + 收發器和您的 10 GbE 網路介面，請使用提供的 QSFP-SFP + 配接器。</span><span class="sxs-lookup"><span data-stu-id="b44c5-316">If using SFP+ transceivers with your 10 GbE network interfaces, use the provided QSFP-SFP+ adapters.</span></span> <span data-ttu-id="b44c5-317">如需詳細資訊，請移至 [10 GbE 網路介面在 StorSimple 裝置上支援的硬體](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-317">For more information, go to [Supported hardware for the 10 GbE network interfaces on your StorSimple device](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).</span></span>
> 
> 

### <a name="serial-port-cabling"></a><span data-ttu-id="b44c5-318">序列連接埠佈線</span><span class="sxs-lookup"><span data-stu-id="b44c5-318">Serial port cabling</span></span>
<span data-ttu-id="b44c5-319">請執行下列步驟，以佈線您的序列連接埠。</span><span class="sxs-lookup"><span data-stu-id="b44c5-319">Perform the following steps to cable your serial port.</span></span>

#### <a name="to-cable-for-serial-connection"></a><span data-ttu-id="b44c5-320">佈線序列連線</span><span class="sxs-lookup"><span data-stu-id="b44c5-320">To cable for serial connection</span></span>
1. <span data-ttu-id="b44c5-321">您的裝置在每個控制器上有以扳手圖示識別的序列連接埠。</span><span class="sxs-lookup"><span data-stu-id="b44c5-321">Your device has a serial port on each controller that is identified by a wrench icon.</span></span> <span data-ttu-id="b44c5-322">若要找出序列連接埠的位置，請參閱顯示裝置背面資料連接埠的圖例。</span><span class="sxs-lookup"><span data-stu-id="b44c5-322">To locate the serial ports, refer to the illustration that shows the data ports on the back of your device.</span></span>
2. <span data-ttu-id="b44c5-323">識別您的裝置後檔板上的作用中控制器。</span><span class="sxs-lookup"><span data-stu-id="b44c5-323">Identify the active controller on your device backplane.</span></span> <span data-ttu-id="b44c5-324">閃爍的的藍色 LED 表示控制器作用中。</span><span class="sxs-lookup"><span data-stu-id="b44c5-324">A blinking blue LED indicates that the controller is active.</span></span>
3. <span data-ttu-id="b44c5-325">使用提供的序列纜線 (如果需要，使用您的膝上型電腦的 USB-序列轉換器)，並將主控台或電腦 (具有裝置的終端機模擬) 連接到作用中控制器的序列連接埠。</span><span class="sxs-lookup"><span data-stu-id="b44c5-325">Use the provided serial cable (if needed, the USB-serial converter for your laptop), and connect your console or computer (with terminal emulation to the device) to the serial port of the active controller.</span></span>
4. <span data-ttu-id="b44c5-326">在電腦上安裝序列-USB 驅動程式 (隨附於裝置)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-326">Install the serial-USB drivers (shipped with the device) on your computer.</span></span>
5. <span data-ttu-id="b44c5-327">設定序列連線，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b44c5-327">Set up the serial connection as follows:</span></span>
   
   * <span data-ttu-id="b44c5-328">115,200 傳輸速率</span><span class="sxs-lookup"><span data-stu-id="b44c5-328">115,200 baud</span></span>
   * <span data-ttu-id="b44c5-329">8 資料位元</span><span class="sxs-lookup"><span data-stu-id="b44c5-329">8 data bits</span></span>
   * <span data-ttu-id="b44c5-330">1 停止位元</span><span class="sxs-lookup"><span data-stu-id="b44c5-330">1 stop bit</span></span>
   * <span data-ttu-id="b44c5-331">無同位檢查</span><span class="sxs-lookup"><span data-stu-id="b44c5-331">No parity</span></span>
   * <span data-ttu-id="b44c5-332">流量控制設為  **無**</span><span class="sxs-lookup"><span data-stu-id="b44c5-332">Flow control set to **None**</span></span>
6. <span data-ttu-id="b44c5-333">藉由在主控台上按下 Enter 鍵，驗證連線是否正在運作。</span><span class="sxs-lookup"><span data-stu-id="b44c5-333">Verify that the connection is working by pressing Enter on the console.</span></span> <span data-ttu-id="b44c5-334">序列主控台功能表應該會出現。</span><span class="sxs-lookup"><span data-stu-id="b44c5-334">A serial console menu should appear.</span></span>

> [!NOTE]
> <span data-ttu-id="b44c5-335">**熄燈管理** ：當裝置安裝在遠端資料中心或在具有限制存取的電腦室時，請確定兩個控制器的序列連接一律會連線至序列主控台交換器或類似的設備。</span><span class="sxs-lookup"><span data-stu-id="b44c5-335">**Lights-Out Management:** When the device is installed in a remote datacenter or in a computer room with limited access, ensure that the serial connections to both controllers are always connected to a serial console switch or similar equipment.</span></span> <span data-ttu-id="b44c5-336">如此可以在網路中斷或非預期失敗時允許頻外遠端控制和支援作業。</span><span class="sxs-lookup"><span data-stu-id="b44c5-336">This allows out-of-band remote control and support operations in case of network disruption or unexpected failures.</span></span>
> 
> 

<span data-ttu-id="b44c5-337">您已經完成您的裝置的電源、網路存取及序列連線的佈線。下一步是設定您的裝置上的軟體。</span><span class="sxs-lookup"><span data-stu-id="b44c5-337">You have completed cabling your device for power, network access, and serial connection.The next step is to configure the software on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b44c5-338">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b44c5-338">Next steps</span></span>
<span data-ttu-id="b44c5-339">您現在已準備好[部署和設定您的內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="b44c5-339">You are now ready to [deploy and configure your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span>

