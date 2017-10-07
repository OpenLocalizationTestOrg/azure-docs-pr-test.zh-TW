---
title: "StorSimple 8000 系列裝置上的 aaaReplace 底座 |Microsoft 文件"
description: "描述如何 tooremove 和取代 hello StorSimple 主要機箱或 EBOD 機箱的底座。"
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
ms.openlocfilehash: 94bbd3d354a9b8866ece036238927e67ec5ce2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="64928-103">取代您的 StorSimple 裝置上的 hello 底座</span><span class="sxs-lookup"><span data-stu-id="64928-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="64928-104">概觀</span><span class="sxs-lookup"><span data-stu-id="64928-104">Overview</span></span>
<span data-ttu-id="64928-105">本教學課程說明如何 tooremove 和取代 StorSimple 8000 系列裝置中的底座。</span><span class="sxs-lookup"><span data-stu-id="64928-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="64928-106">hello StorSimple 8100 模型是單一機箱裝置 （一個底座），而 hello 8600 是雙重機箱裝置 （兩個底座）。</span><span class="sxs-lookup"><span data-stu-id="64928-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="64928-107">8600 模型中，有可能兩個底座 hello 裝置中可能會失敗： hello hello 主要機箱的底座或 hello hello EBOD 機箱的底座。</span><span class="sxs-lookup"><span data-stu-id="64928-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="64928-108">在任一情況下，Microsoft 提供的 hello 取代底座是空的。</span><span class="sxs-lookup"><span data-stu-id="64928-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="64928-109">將不會包含電源和冷卻模組 (PCM)、控制器模組、固態硬碟 (SSD)、硬碟機 (HDD) 或 EBOD 模組。</span><span class="sxs-lookup"><span data-stu-id="64928-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64928-110">移除或取代 hello 底座檢閱中的 hello 安全性資訊之前[StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="64928-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-chassis"></a><span data-ttu-id="64928-111">移除 hello 底座</span><span class="sxs-lookup"><span data-stu-id="64928-111">Remove hello chassis</span></span>
<span data-ttu-id="64928-112">執行下列步驟 tooremove hello 底座 StorSimple 裝置上的 hello。</span><span class="sxs-lookup"><span data-stu-id="64928-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="64928-113">tooremove 底座</span><span class="sxs-lookup"><span data-stu-id="64928-113">tooremove a chassis</span></span>
1. <span data-ttu-id="64928-114">請確定該 hello StorSimple 裝置已關閉，並中斷所有 hello 電源來源。</span><span class="sxs-lookup"><span data-stu-id="64928-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="64928-115">移除所有 hello 網路和 SAS 纜線，如果適用的話。</span><span class="sxs-lookup"><span data-stu-id="64928-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="64928-116">移除 hello 機架 hello 單位。</span><span class="sxs-lookup"><span data-stu-id="64928-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="64928-117">移除每個 hello 磁碟機，並記下移除的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="64928-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="64928-118">如需詳細資訊，請參閱[移除 hello 磁碟機](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive)。</span><span class="sxs-lookup"><span data-stu-id="64928-118">For more information, see [Remove hello disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="64928-119">在 hello EBOD 機箱 （如果這是失敗的 hello 底座），移除 hello EBOD 控制器模組。</span><span class="sxs-lookup"><span data-stu-id="64928-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="64928-120">如需詳細資訊，請參閱 [取下 EBOD 控制器](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller)。</span><span class="sxs-lookup"><span data-stu-id="64928-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="64928-121">在 hello 主要機箱 （如果這是失敗的 hello 底座），移除 hello 控制站並記下 hello 插槽從中移除。</span><span class="sxs-lookup"><span data-stu-id="64928-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="64928-122">如需詳細資訊，請參閱 [取下控制器](storsimple-8000-controller-replacement.md#remove-a-controller)。</span><span class="sxs-lookup"><span data-stu-id="64928-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="64928-123">安裝底座 hello</span><span class="sxs-lookup"><span data-stu-id="64928-123">Install hello chassis</span></span>
<span data-ttu-id="64928-124">執行下列步驟 tooinstall hello 底座 StorSimple 裝置上的 hello。</span><span class="sxs-lookup"><span data-stu-id="64928-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="64928-125">tooinstall 底座</span><span class="sxs-lookup"><span data-stu-id="64928-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="64928-126">掛接 hello 底座 hello 機架中。</span><span class="sxs-lookup"><span data-stu-id="64928-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="64928-127">如需詳細資訊，請參閱[以機架掛接 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device)或[以機架掛接 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device)。</span><span class="sxs-lookup"><span data-stu-id="64928-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="64928-128">Hello 底座 hello 機架中後，請將 hello 控制器模組安裝在相同放置，於先前安裝中的 hello。</span><span class="sxs-lookup"><span data-stu-id="64928-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="64928-129">安裝 hello 磁碟機的 hello 相同的定位和插槽中，於先前安裝中。</span><span class="sxs-lookup"><span data-stu-id="64928-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="64928-130">我們建議您首先，安裝 hello Ssd hello 插槽中，然後再安裝 hello Hdd。</span><span class="sxs-lookup"><span data-stu-id="64928-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
  
4. <span data-ttu-id="64928-131">以 hello hello 機架中掛接裝置和 hello 安裝元件，連接您的裝置 toohello 適當的電源，並開啟 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="64928-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="64928-132">如需詳細資料，請參閱[將您的 StorSimple 8100 裝置接上纜線](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device)或[將您的 StorSimple 8600 裝置接上纜線](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device)。</span><span class="sxs-lookup"><span data-stu-id="64928-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="64928-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64928-133">Next steps</span></span>
<span data-ttu-id="64928-134">深入了解 [StorSimple 硬體元件更換](storsimple-8000-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="64928-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

