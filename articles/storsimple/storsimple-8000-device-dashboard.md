---
title: "StorSimple 8000 系列裝置使用摘要 | Microsoft Docs"
description: "描述 StorSimple 裝置管理員服務裝置摘要，以及如何用它來檢視儲存體計量和連線的啟動器，並尋找序號和 IQN。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 784d3ce9d8f926b00ac1c6fbf48a05c0b04f900a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="7ec0e-103">使用 StorSimple 裝置管理員服務中的裝置摘要</span><span class="sxs-lookup"><span data-stu-id="7ec0e-103">Use the device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="7ec0e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="7ec0e-104">Overview</span></span>
<span data-ttu-id="7ec0e-105">StorSimple 裝置摘要刀鋒視窗可提供特定 StorSimple 裝置的資訊概觀；相對於服務摘要刀鋒視窗，其提供 Microsoft Azure StorSimple 解決方案中所有裝置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-105">The StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast to the service summary blade, which gives you information about all the devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="7ec0e-106">對於已向給定 StorSimple 裝置管理員註冊的 StorSimple 8000 系列裝置，裝置摘要刀鋒視窗提供摘要檢視，並醒目提示需要系統管理員注意的裝置問題。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-106">The device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="7ec0e-107">本教學課程介紹裝置摘要刀鋒視窗、說明內容和功能，並描述您可以從這個刀鋒視窗執行的工作。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-107">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="7ec0e-108">裝置摘要刀鋒視窗會顯示以下資訊：</span><span class="sxs-lookup"><span data-stu-id="7ec0e-108">The device summary blade displays the following information:</span></span>

![[裝置摘要] 刀鋒視窗](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="7ec0e-110">管理命令列</span><span class="sxs-lookup"><span data-stu-id="7ec0e-110">Management command bar</span></span>

<span data-ttu-id="7ec0e-111">在 StorSimple 裝置刀鋒視窗中，您會看到 StorSimple 裝置的管理選項。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-111">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="7ec0e-112">您在刀鋒視窗的上方橫幅和左邊會看到管理命令。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-112">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="7ec0e-113">請使用這些選項來新增共用或磁碟區，或是更新或容錯移轉您的裝置。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-113">Use these options to add shares or volumes, or update or fail over your device.</span></span>

![管理命令列](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="7ec0e-115">基本資訊</span><span class="sxs-lookup"><span data-stu-id="7ec0e-115">Essentials</span></span>

<span data-ttu-id="7ec0e-116">基本資訊區域擷取一些重要屬性，例如狀態、型號、目標 IQN，以及軟體版本。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-116">The essentials area captures some of the important properties such as, the status, model, target IQN, and the software version.</span></span> 

![裝置的基本資訊](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="7ec0e-118">監視</span><span class="sxs-lookup"><span data-stu-id="7ec0e-118">Monitoring</span></span>

* <span data-ttu-id="7ec0e-119">[警示] 圖格提供裝置之所有作用中警示的快照 (依警示嚴重性分組)。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-119">The **Alerts** tile provides a snapshot of all the active alerts for your device, grouped by alert severity.</span></span>

    ![警示圖格](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="7ec0e-121">按一下此圖格來開啟 [警示] 刀鋒視窗，然後按一下個別警示來檢視該警示的其他詳細資料，包括任何建議的動作。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-121">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="7ec0e-122">如果已解決問題，您也可以清除警示。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-122">You can also clear the alert if the issue has been resolved.</span></span>

    ![按一下 [警示] 圖格](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="7ec0e-124">[狀態與健康情況] 圖格可讓您深入了解裝置的硬體元件健康情況，包含裝置狀態。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-124">The **Status and health** tile provides insights into the hardware component health for a device including the device status.</span></span> <span data-ttu-id="7ec0e-125">裝置狀態可能是離線、線上、停用，或設定就緒。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-125">The device status may be offline, online, deactivated, or ready to set up.</span></span>

    ![狀態與健康情況圖格](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="7ec0e-127">[磁碟區] 圖格提供裝置中依狀態分組的磁碟區數目摘要。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-127">The **Volumes** tile provides a summary of the number of volumes in your device grouped by status.</span></span>

    ![磁碟區圖格](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="7ec0e-129">按一下此圖格來開啟 [磁碟區] 清單刀鋒視窗，然後按一下個別磁碟區來檢視或修改其屬性。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-129">Click the tile to open the **Volumes** list blade, and then click on an individual volume to view or modify its properties.</span></span>
    
    ![按一下 [磁碟區] 圖格](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="7ec0e-131">如需詳細資訊，請參閱[如何管理磁碟區](storsimple-8000-manage-volumes-u2.md)。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-131">For more information, see how to [manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="7ec0e-132">在 [使用量] 圖表中，您可以檢視整個裝置已使用的主要儲存空間，以及過去 7 天 (預設期間) 耗用的雲端儲存空間。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-132">In the **Usage** chart, you can view the primary storage used across your device, and the cloud storage consumed over the past 7 days, the default time period.</span></span>

     ![使用量圖格](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="7ec0e-134">若要選擇不同的時間間隔，請使用圖表右上角的 [編輯] 選項。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-134">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![編輯使用量圖表](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="7ec0e-136">在此圖表中，您可以檢視主要儲存體總計 (主機寫入至您的裝置的資料數量) 和您的裝置一段時間內所使用的雲端儲存體總計的度量資訊。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-136">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="7ec0e-137">在此情況下，「主要儲存體」是指由主機寫入的資料總量，並可依磁碟區類型細分︰「主要階層式存放區」包含在本機儲存的資料和分層至雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-137">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud.</span></span> <span data-ttu-id="7ec0e-138">「主要本機釘選儲存體」只包含在本機儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="7ec0e-139">相反地，「雲端儲存體」是儲存在雲端中的資料總量測量。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-139">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="7ec0e-140">此儲存體包括分層式資料和備份。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="7ec0e-141">儲存在雲端中的資料會進行重複資料刪除和壓縮，而主要儲存體會指出進行重複資料刪除和壓縮之前已使用的儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-141">The data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="7ec0e-142">(您可以比較這兩個數字以了解壓縮率)。對於主要和雲端儲存體，所顯示的數量會以您設定的追蹤頻率為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-142">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown are based on the tracking frequency you configure.</span></span> <span data-ttu-id="7ec0e-143">例如，如果您選擇一週頻率，則此圖表會顯示上週每一天的資料。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-143">For example, if you choose a one week frequency, then the chart shows data for each day in the previous week.</span></span>

     <span data-ttu-id="7ec0e-144">若要查看一段時間耗用的雲端儲存體數量，請選取 [ **使用的雲端儲存體** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-144">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="7ec0e-145">若要查看主機所寫入的儲存體總量，請選取 [使用的主要分層式儲存體] 和 [使用的本機釘選儲存體] 選項。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-145">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="7ec0e-146">如需詳細資訊，請參閱[使用 StorSimple 裝置管理員服務監視 StorSimple 裝置](storsimple-monitor-device.md)。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-146">For more information, see [Use the StorSimple Device Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="7ec0e-147">[容量] 圖格顯示裝置上相對於可用的總儲存空間而言，已佈建和剩餘的主要儲存空間。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-147">The **Capacity** tile displays the primary storage that is provisioned and remaining across the device relative to the total storage available for the same.</span></span> <span data-ttu-id="7ec0e-148">[已佈建] 是指已備妥和配置供使用的儲存空間數量，[剩餘] 是指這個裝置上可佈建的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-148">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> 

    ![使用量圖格](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="7ec0e-150">按一下此圖格以檢視如何在分層式磁碟區和固定在本機的磁碟區佈建容量。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-150">Click this tile to view how the capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="7ec0e-151">[剩餘階層式] 容量是可供佈建的容量，包括雲端，而 [剩餘本機] 是連接至此裝置的磁碟上剩餘的容量。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-151">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this device.</span></span>

    ![按一下 [使用量] 圖表](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="7ec0e-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ec0e-153">Next steps</span></span>
* <span data-ttu-id="7ec0e-154">深入了解 [StorSimple 服務摘要刀鋒視窗](storsimple-8000-service-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-154">Learn more about the [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="7ec0e-155">深入了解[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="7ec0e-155">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

