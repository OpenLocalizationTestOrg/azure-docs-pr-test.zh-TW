---
title: "aaaReplace StorSimple 裝置上的磁碟機 |Microsoft 文件"
description: "說明 tooreplace 磁碟 StorSimple 主要機箱或 EBOD 機箱上的磁碟機。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="2cd86-103">更換 StorSimple 裝置上的磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="2cd86-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2cd86-104">Overview</span></span>
<span data-ttu-id="2cd86-105">本教學課程說明如何取下和更換 Microsoft Azure StorSimple 裝置上無法運作或故障的硬碟。</span><span class="sxs-lookup"><span data-stu-id="2cd86-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="2cd86-106">tooreplace 磁碟機，您要：</span><span class="sxs-lookup"><span data-stu-id="2cd86-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="2cd86-107">卸除 hello 防拆鎖</span><span class="sxs-lookup"><span data-stu-id="2cd86-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="2cd86-108">移除 hello 磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-108">Remove hello disk drive</span></span>
* <span data-ttu-id="2cd86-109">安裝 hello 更換磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cd86-110">移除和更換磁碟機，請檢閱中的 hello 安全資訊之前[StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="2cd86-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="2cd86-111">卸除 hello 防拆鎖</span><span class="sxs-lookup"><span data-stu-id="2cd86-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="2cd86-112">此程序說明如何 hello StorSimple 裝置上的防拆鎖可以囓合或當您取代 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2cd86-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="2cd86-113">hello 防拆鎖會納入在 hello 磁碟機托架把手，並透過小孔 hello 控制代碼的 hello 閂鎖區段中存取它們。</span><span class="sxs-lookup"><span data-stu-id="2cd86-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="2cd86-114">Hello 鎖定組 toohello 鎖定位置提供磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2cd86-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="2cd86-115">toounlock hello 防拆鎖</span><span class="sxs-lookup"><span data-stu-id="2cd86-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="2cd86-116">Hello 控制代碼中的 hello 光圈和它的通訊端，小心地將 hello 鎖定鑰匙 （「 防拆 」 T10 螺絲起子 Microsoft 提供）。</span><span class="sxs-lookup"><span data-stu-id="2cd86-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2cd86-117">如果已啟動 hello 防拆鎖，hello 紅色指示器中會顯示 hello 光圈。</span><span class="sxs-lookup"><span data-stu-id="2cd86-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
   > 
   > 
   
    ![已鎖定磁碟機](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="2cd86-119">**圖 1** 防拆鎖已扣上</span><span class="sxs-lookup"><span data-stu-id="2cd86-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="2cd86-120">標籤</span><span class="sxs-lookup"><span data-stu-id="2cd86-120">Label</span></span> | <span data-ttu-id="2cd86-121">說明</span><span class="sxs-lookup"><span data-stu-id="2cd86-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2cd86-122">1</span><span class="sxs-lookup"><span data-stu-id="2cd86-122">1</span></span> |<span data-ttu-id="2cd86-123">指示器孔</span><span class="sxs-lookup"><span data-stu-id="2cd86-123">Indicator aperture</span></span> |
   | <span data-ttu-id="2cd86-124">2</span><span class="sxs-lookup"><span data-stu-id="2cd86-124">2</span></span> |<span data-ttu-id="2cd86-125">防拆鎖</span><span class="sxs-lookup"><span data-stu-id="2cd86-125">Antitamper lock</span></span> |
2. <span data-ttu-id="2cd86-126">直到 hello 紅色指示器中未顯示 hello 光圈上方 hello 金鑰以逆時針方向旋轉 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2cd86-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="2cd86-127">移除 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2cd86-127">Remove hello key.</span></span>
   
    ![已解除鎖定磁碟機](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="2cd86-129">**圖 2** 已解除鎖定磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="2cd86-130">現在即可卸下 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2cd86-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="2cd86-131">步驟 hello 反向 tooengage hello 鎖定中。</span><span class="sxs-lookup"><span data-stu-id="2cd86-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="2cd86-132">移除 hello 磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-132">Remove hello disk drive</span></span>
<span data-ttu-id="2cd86-133">您的 StorSimple 裝置支援如 RAID 10 的儲存空間組態。</span><span class="sxs-lookup"><span data-stu-id="2cd86-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="2cd86-134">這表示它可以在一個磁碟、固態硬碟 (SSD) 或硬碟 (HDD) 故障的情況下正常操作。</span><span class="sxs-lookup"><span data-stu-id="2cd86-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="2cd86-135">如果您的系統有一個以上的故障的磁碟，不要移除一個以上的 SSD 或 HDD hello 系統在任何時間點的時間。</span><span class="sxs-lookup"><span data-stu-id="2cd86-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="2cd86-136">這樣做可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="2cd86-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="2cd86-137">請確定您將更換 SSD 放置在先前包含 SSD 的插槽中。</span><span class="sxs-lookup"><span data-stu-id="2cd86-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="2cd86-138">同樣地，請將更換 HDD 放置在先前包含 HDD 的插槽中。</span><span class="sxs-lookup"><span data-stu-id="2cd86-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="2cd86-139">在 hello Azure 傳統入口網站，插槽編號為 0 – 11。</span><span class="sxs-lookup"><span data-stu-id="2cd86-139">In hello Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="2cd86-140">因此，如果 hello 入口網站顯示插槽 2 中的磁碟已經失敗，hello 裝置上尋找 hello hello 第三個位置中的故障磁碟從 hello 左上角。</span><span class="sxs-lookup"><span data-stu-id="2cd86-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="2cd86-141">磁碟機可以移除並取代 hello 系統運作時。</span><span class="sxs-lookup"><span data-stu-id="2cd86-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="2cd86-142">tooremove 磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-142">tooremove a drive</span></span>
1. <span data-ttu-id="2cd86-143">tooidentify hello 故障的磁碟，請在 hello Azure 傳統入口網站中移過**裝置** > **維護** > **硬體狀態**。</span><span class="sxs-lookup"><span data-stu-id="2cd86-143">tooidentify hello failed disk, in hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="2cd86-144">因為磁碟可能會失敗，在 hello 主要機箱和/或 EBOD 機箱 （如果您正使用 8600 模型） 中，查看 hello 狀態下的 hello 磁碟**共用元件**下方和  **EBOD 機箱共用元件**.</span><span class="sxs-lookup"><span data-stu-id="2cd86-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="2cd86-145">任一機箱中故障的磁碟將以紅色狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="2cd86-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="2cd86-146">Hello 正面 hello 主要機箱或 hello EBOD 機箱中，找出 hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2cd86-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="2cd86-147">如果 hello 磁碟已解除鎖定，繼續 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="2cd86-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="2cd86-148">如果 hello 磁碟已鎖定，依照下列中的 hello 程序解除鎖定[解除 hello 防拆鎖](#disengage-the-antitamper-lock)。</span><span class="sxs-lookup"><span data-stu-id="2cd86-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="2cd86-149">按 hello 黑色上 hello 磁碟機載具模組閂鎖，而從 hello 底座 hello 前端逾時，立即提取 hello 磁碟機托架把手。</span><span class="sxs-lookup"><span data-stu-id="2cd86-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span> 
   
    ![鬆開磁碟機把手](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="2cd86-151">**圖 3**釋放 hello 磁碟機把手</span><span class="sxs-lookup"><span data-stu-id="2cd86-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="2cd86-152">當 hello 磁碟機托架把手完全延伸，投影片 hello 磁碟機托架超出 hello 底座。</span><span class="sxs-lookup"><span data-stu-id="2cd86-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![將磁碟滑出磁碟機](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="2cd86-154">**圖 4**滑動 hello hello 載波偵測出的磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="2cd86-155">安裝 hello 更換磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="2cd86-156">StorSimple 裝置中故障磁碟機，並將它卸下之後，請遵循此程序 tooreplace 它與新的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="2cd86-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="2cd86-157">tooinsert 磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-157">tooinsert a drive</span></span>
1. <span data-ttu-id="2cd86-158">請確定 hello 磁碟機托架把手完全延伸，hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="2cd86-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![把手已伸展的磁碟機](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="2cd86-160">**圖 5** 把手已伸展的磁碟機</span><span class="sxs-lookup"><span data-stu-id="2cd86-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="2cd86-161">Hello 所有 hello 方式的磁碟機托架滑入 hello 底座中。</span><span class="sxs-lookup"><span data-stu-id="2cd86-161">Slide hello drive carrier all hello way into hello chassis.</span></span> 
   
    ![將磁碟滑入磁碟機載具](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="2cd86-163">**圖 6**滑動 hello 磁碟機托架至 hello 底座</span><span class="sxs-lookup"><span data-stu-id="2cd86-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="2cd86-164">與 hello 磁碟機托架插入，請關閉 hello 磁碟機托架把手時繼續 toopush hello 磁碟機托架至 hello 底座，直到 hello 磁碟機托架把手扣入鎖定的位置。</span><span class="sxs-lookup"><span data-stu-id="2cd86-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="2cd86-165">由 Microsoft （防拆 Torx 螺絲起子） toosecure hello 托架把手位置提供藉由開啟 hello 鎖定螺絲四分之一順時針使用 hello lock 鍵。</span><span class="sxs-lookup"><span data-stu-id="2cd86-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="2cd86-166">確認 hello 更換成功，而且 hello 磁碟機操作存取 hello Azure 傳統入口網站，並巡覽太**維護** > **硬體狀態**。</span><span class="sxs-lookup"><span data-stu-id="2cd86-166">Verify that hello replacement was successful and hello drive is operational by accessing hello Azure classic portal and navigating too**Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="2cd86-167">在下**共用元件**或**EBOD 機箱共用元件**，hello 磁碟機狀態應為綠色，表示運作正常。</span><span class="sxs-lookup"><span data-stu-id="2cd86-167">Under **Shared Components** or **EBOD enclosure Shared Components**, hello drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2cd86-168">它可能需要幾個小時 hello 磁碟狀態 tooturn 綠色之後 hello 取代。</span><span class="sxs-lookup"><span data-stu-id="2cd86-168">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="2cd86-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2cd86-169">Next steps</span></span>
<span data-ttu-id="2cd86-170">深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="2cd86-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

