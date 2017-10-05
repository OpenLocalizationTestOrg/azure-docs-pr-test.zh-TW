---
title: "更換 StorSimple 8000 系列裝置上的底座 | Microsoft Docs"
description: "描述如何移除並更換 StorSimple 主要機箱或 EBOD 機箱的底座。"
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 073fcf0064f1d1482f4683d733f00cf918ff2f38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="8087a-103">更換 StorSimple 裝置上的底座</span><span class="sxs-lookup"><span data-stu-id="8087a-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="8087a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8087a-104">Overview</span></span>
<span data-ttu-id="8087a-105">本教學課程說明如何取下並更換 StorSimple 8000 系列裝置中的底座。</span><span class="sxs-lookup"><span data-stu-id="8087a-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="8087a-106">StorSimple 8100 模型是單一機箱裝置 (一個底座)，而 8600 是雙重機箱裝置 (兩個底座)。</span><span class="sxs-lookup"><span data-stu-id="8087a-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="8087a-107">若為 8600 型號，裝置中可能有兩個會發生故障的底座：主要機箱的底座或 EBOD 機箱的底座。</span><span class="sxs-lookup"><span data-stu-id="8087a-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="8087a-108">在任一情況下，Microsoft 隨附的更換底座是空的。</span><span class="sxs-lookup"><span data-stu-id="8087a-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="8087a-109">將不會包含電源和冷卻模組 (PCM)、控制器模組、固態硬碟 (SSD)、硬碟機 (HDD) 或 EBOD 模組。</span><span class="sxs-lookup"><span data-stu-id="8087a-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8087a-110">取下並更換底座之前，請閱讀 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)中的安全資訊。</span><span class="sxs-lookup"><span data-stu-id="8087a-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-chassis"></a><span data-ttu-id="8087a-111">取下底座</span><span class="sxs-lookup"><span data-stu-id="8087a-111">Remove the chassis</span></span>
<span data-ttu-id="8087a-112">請執行下列步驟來取下 StorSimple 裝置上的底座。</span><span class="sxs-lookup"><span data-stu-id="8087a-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="8087a-113">若要取下底座</span><span class="sxs-lookup"><span data-stu-id="8087a-113">To remove a chassis</span></span>
1. <span data-ttu-id="8087a-114">確認 StorSimple 裝置已關閉，並與所有電源中斷連接。</span><span class="sxs-lookup"><span data-stu-id="8087a-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="8087a-115">取下所有網路和 SAS 纜線 (如果適當的話)。</span><span class="sxs-lookup"><span data-stu-id="8087a-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="8087a-116">取下機架中的裝置。</span><span class="sxs-lookup"><span data-stu-id="8087a-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="8087a-117">取下每個磁碟機，並記下從哪些插槽中取下它們。</span><span class="sxs-lookup"><span data-stu-id="8087a-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="8087a-118">如需詳細資訊，請參閱 [取下磁碟機](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive)。</span><span class="sxs-lookup"><span data-stu-id="8087a-118">For more information, see [Remove the disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="8087a-119">在 EBOD 機箱 (如果這是故障的底座) 上，取下 EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="8087a-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="8087a-120">如需詳細資訊，請參閱 [取下 EBOD 控制器](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller)。</span><span class="sxs-lookup"><span data-stu-id="8087a-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="8087a-121">在主要機箱 (如果這是故障的底座) 上，取下控制器，並記下從哪些插槽中取下它們。</span><span class="sxs-lookup"><span data-stu-id="8087a-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="8087a-122">如需詳細資訊，請參閱 [取下控制器](storsimple-8000-controller-replacement.md#remove-a-controller)。</span><span class="sxs-lookup"><span data-stu-id="8087a-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="8087a-123">安裝底座</span><span class="sxs-lookup"><span data-stu-id="8087a-123">Install the chassis</span></span>
<span data-ttu-id="8087a-124">請執行下列步驟來安裝 StorSimple 裝置上的底座。</span><span class="sxs-lookup"><span data-stu-id="8087a-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="8087a-125">若要安裝底座</span><span class="sxs-lookup"><span data-stu-id="8087a-125">To install a chassis</span></span>
1. <span data-ttu-id="8087a-126">以機架掛接底座。</span><span class="sxs-lookup"><span data-stu-id="8087a-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="8087a-127">如需詳細資訊，請參閱[以機架掛接 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device)或[以機架掛接 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device)。</span><span class="sxs-lookup"><span data-stu-id="8087a-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="8087a-128">在以機架掛接了底座之後，請將控制器模組安裝在先前安裝它們的同一位置中。</span><span class="sxs-lookup"><span data-stu-id="8087a-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="8087a-129">將磁碟機安裝在先前安裝它們的同一位置和插槽中。</span><span class="sxs-lookup"><span data-stu-id="8087a-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8087a-130">我們建議您先將 SSD 安裝於插槽中，然後再安裝 HDD。</span><span class="sxs-lookup"><span data-stu-id="8087a-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
  
4. <span data-ttu-id="8087a-131">在以機架掛接裝置，並安裝元件之後，請將裝置連接至適當的電源，並開啟裝置。</span><span class="sxs-lookup"><span data-stu-id="8087a-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="8087a-132">如需詳細資料，請參閱[將您的 StorSimple 8100 裝置接上纜線](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device)或[將您的 StorSimple 8600 裝置接上纜線](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)。</span><span class="sxs-lookup"><span data-stu-id="8087a-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8087a-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8087a-133">Next steps</span></span>
<span data-ttu-id="8087a-134">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="8087a-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

