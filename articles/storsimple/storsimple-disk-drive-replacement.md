---
title: "更換 StorSimple 裝置上的磁碟機 | Microsoft Docs"
description: "說明如何更換 StorSimple 主要機箱或 EBOD 機箱上的磁碟機。"
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
ms.openlocfilehash: 0659ab9d304dbfcce72e8c3c79edad68e70b9630
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="953ea-103">更換 StorSimple 裝置上的磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="953ea-104">Overview</span><span class="sxs-lookup"><span data-stu-id="953ea-104">Overview</span></span>
<span data-ttu-id="953ea-105">本教學課程說明如何取下和更換 Microsoft Azure StorSimple 裝置上無法運作或故障的硬碟。</span><span class="sxs-lookup"><span data-stu-id="953ea-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="953ea-106">若要取下磁碟機，您必須：</span><span class="sxs-lookup"><span data-stu-id="953ea-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="953ea-107">打開防拆鎖</span><span class="sxs-lookup"><span data-stu-id="953ea-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="953ea-108">取下磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-108">Remove the disk drive</span></span>
* <span data-ttu-id="953ea-109">安裝更換磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="953ea-110">取下及更換磁碟機之前，請閱讀 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)中的安全資訊。</span><span class="sxs-lookup"><span data-stu-id="953ea-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="953ea-111">打開防拆鎖</span><span class="sxs-lookup"><span data-stu-id="953ea-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="953ea-112">此程序說明在更換磁碟機時如何扣上或打開 StorSimple 裝置上的防拆鎖。</span><span class="sxs-lookup"><span data-stu-id="953ea-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="953ea-113">防拆鎖固定在磁碟機的載具把手，而且它們是透過把手的閂鎖部件中的小孔來存取。</span><span class="sxs-lookup"><span data-stu-id="953ea-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="953ea-114">提供磁碟機時已將鎖設定為鎖定的位置。</span><span class="sxs-lookup"><span data-stu-id="953ea-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="953ea-115">若要解除鎖定防拆鎖</span><span class="sxs-lookup"><span data-stu-id="953ea-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="953ea-116">小心地將鎖鑰匙 (Microsoft 提供的「防拆」T10 螺絲起子) 插入把手中的孔中，並插入其插座中。</span><span class="sxs-lookup"><span data-stu-id="953ea-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="953ea-117">如果防拆鎖已啟動，則可在孔中看到紅色指示器。</span><span class="sxs-lookup"><span data-stu-id="953ea-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![已鎖定磁碟機](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="953ea-119">**圖 1** 防拆鎖已扣上</span><span class="sxs-lookup"><span data-stu-id="953ea-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="953ea-120">標籤</span><span class="sxs-lookup"><span data-stu-id="953ea-120">Label</span></span> | <span data-ttu-id="953ea-121">說明</span><span class="sxs-lookup"><span data-stu-id="953ea-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="953ea-122">1</span><span class="sxs-lookup"><span data-stu-id="953ea-122">1</span></span> |<span data-ttu-id="953ea-123">指示器孔</span><span class="sxs-lookup"><span data-stu-id="953ea-123">Indicator aperture</span></span> |
   | <span data-ttu-id="953ea-124">2</span><span class="sxs-lookup"><span data-stu-id="953ea-124">2</span></span> |<span data-ttu-id="953ea-125">防拆鎖</span><span class="sxs-lookup"><span data-stu-id="953ea-125">Antitamper lock</span></span> |
2. <span data-ttu-id="953ea-126">以逆時鐘方向旋轉鑰匙，直到在鑰匙上方的孔中看不到紅色指示器。</span><span class="sxs-lookup"><span data-stu-id="953ea-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="953ea-127">取下鑰匙。</span><span class="sxs-lookup"><span data-stu-id="953ea-127">Remove the key.</span></span>
   
    ![已解除鎖定磁碟機](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="953ea-129">**圖 2** 已解除鎖定磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="953ea-130">現在可以取下磁碟機。</span><span class="sxs-lookup"><span data-stu-id="953ea-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="953ea-131">請反向依照步驟來扣上鎖。</span><span class="sxs-lookup"><span data-stu-id="953ea-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="953ea-132">取下磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-132">Remove the disk drive</span></span>
<span data-ttu-id="953ea-133">您的 StorSimple 裝置支援如 RAID 10 的儲存空間組態。</span><span class="sxs-lookup"><span data-stu-id="953ea-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="953ea-134">這表示它可以在一個磁碟、固態硬碟 (SSD) 或硬碟 (HDD) 故障的情況下正常操作。</span><span class="sxs-lookup"><span data-stu-id="953ea-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="953ea-135">如果您的系統有一個以上故障的磁碟，請勿於任何時間點從系統移除一個以上的 SSD 或 HDD。</span><span class="sxs-lookup"><span data-stu-id="953ea-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="953ea-136">這樣做可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="953ea-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="953ea-137">請確定您將更換 SSD 放置在先前包含 SSD 的插槽中。</span><span class="sxs-lookup"><span data-stu-id="953ea-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="953ea-138">同樣地，請將更換 HDD 放置在先前包含 HDD 的插槽中。</span><span class="sxs-lookup"><span data-stu-id="953ea-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="953ea-139">在傳統入口網站中，插槽的編號從 0 – 11。</span><span class="sxs-lookup"><span data-stu-id="953ea-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="953ea-140">因此，如果入口網站顯示插槽 2 中的磁碟故障，請在裝置上從左上角算起的第三個插槽中尋找故障的磁碟。</span><span class="sxs-lookup"><span data-stu-id="953ea-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="953ea-141">您可以在系統操作時取下和更換磁碟機。</span><span class="sxs-lookup"><span data-stu-id="953ea-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="953ea-142">若要取下磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-142">To remove a drive</span></span>
1. <span data-ttu-id="953ea-143">若要識別故障的磁碟，請在 Azure 傳統入口網站中，移至 [裝置]  >  [維護]  >  [硬體狀態]。</span><span class="sxs-lookup"><span data-stu-id="953ea-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="953ea-144">因為主要機箱和/或 EBOD 機箱 (如果您是使用 8600 機型) 中的磁碟可能故障，請查看 [共用元件] 和 [EBOD 機箱共用元件] 下的磁碟狀態。</span><span class="sxs-lookup"><span data-stu-id="953ea-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="953ea-145">任一機箱中故障的磁碟將以紅色狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="953ea-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="953ea-146">找出主要機箱或 EBOD 機箱前面的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="953ea-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="953ea-147">如果磁碟已解除鎖定，請繼續下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="953ea-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="953ea-148">如果磁碟已鎖定，請遵循 [打開防拆鎖](#disengage-the-antitamper-lock)中的程序，將它解除鎖定。</span><span class="sxs-lookup"><span data-stu-id="953ea-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="953ea-149">按壓磁碟機載具模組上的黑色閂鎖，然後拉出磁碟機載具把手，並從底座前端移走。</span><span class="sxs-lookup"><span data-stu-id="953ea-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![鬆開磁碟機把手](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="953ea-151">**圖 3** 鬆開磁碟機把手</span><span class="sxs-lookup"><span data-stu-id="953ea-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="953ea-152">當磁碟機載具把手完全伸展時，請將磁碟機載具滑出底座。</span><span class="sxs-lookup"><span data-stu-id="953ea-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![將磁碟滑出磁碟機](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="953ea-154">**圖 4** 將磁碟機滑出載具</span><span class="sxs-lookup"><span data-stu-id="953ea-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="953ea-155">安裝更換磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-155">Install the replacement disk drive</span></span>
<span data-ttu-id="953ea-156">在 StorSimple 裝置中的磁碟機故障，而且您已取下它之後，請遵循此程序，將它更換為新的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="953ea-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="953ea-157">若要插入磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-157">To insert a drive</span></span>
1. <span data-ttu-id="953ea-158">確定磁碟機載具把手已完全伸展，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="953ea-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![把手已伸展的磁碟機](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="953ea-160">**圖 5** 把手已伸展的磁碟機</span><span class="sxs-lookup"><span data-stu-id="953ea-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="953ea-161">將磁碟機載具完全滑入底座。</span><span class="sxs-lookup"><span data-stu-id="953ea-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![將磁碟滑入磁碟機載具](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="953ea-163">**圖 6** 將磁碟機載具滑入底座</span><span class="sxs-lookup"><span data-stu-id="953ea-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="953ea-164">一旦插入磁碟機載具，請關閉磁碟機載具把手，同時繼續將磁碟機載具推入底座，直到磁碟機載具把手卡入鎖定的位置。</span><span class="sxs-lookup"><span data-stu-id="953ea-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="953ea-165">使用 Microsoft 所提供的鎖鑰匙 (防拆 Torx 螺絲起子)，將鎖螺絲順時鐘方向旋轉四分之一來固定住載具把手。</span><span class="sxs-lookup"><span data-stu-id="953ea-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="953ea-166">存取 Azure 傳統入口網站，並導覽至 [維護]  >  [硬體狀態]，來確認更換成功，而且磁碟機可運作。</span><span class="sxs-lookup"><span data-stu-id="953ea-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="953ea-167">在 [共用元件] 或 [EBOD 機箱共用元件] 下，磁碟機狀態應該是綠色,表示狀況良好。</span><span class="sxs-lookup"><span data-stu-id="953ea-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="953ea-168">在更換之後，可能需要數小時，磁碟狀態才會變成綠色。</span><span class="sxs-lookup"><span data-stu-id="953ea-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="953ea-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="953ea-169">Next steps</span></span>
<span data-ttu-id="953ea-170">深入了解 [StorSimple 硬體元件更換](storsimple-hardware-component-replacement.md)。</span><span class="sxs-lookup"><span data-stu-id="953ea-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

