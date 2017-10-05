---
title: "StorSimple 8000 系列裝置使用摘要 | Microsoft Docs"
description: "描述 StorSimple 的 [服務摘要] 刀鋒視窗，並說明如何使用它來監視 StorSimple 解決方案的健全狀況。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: d987a4ae170f21532a886552cbe1eb5a0d25fc3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-8000-series-device"></a><span data-ttu-id="bce38-103">使用 StorSimple 8000 系列裝置的 [服務摘要] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="bce38-103">Use the service summary blade for StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="bce38-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bce38-104">Overview</span></span>

<span data-ttu-id="bce38-105">StorSimple 裝置管理員的 [服務摘要] 刀鋒視窗提供連線至 StorSimple 裝置管理員服務之所有裝置的摘要檢視，並強調顯示需要系統管理員注意的裝置。</span><span class="sxs-lookup"><span data-stu-id="bce38-105">The StorSimple Device Manager service summary blade provides a summary view of all the devices that are connected to the StorSimple Device Manager service, highlighting those devices that need a system administrator's attention.</span></span> <span data-ttu-id="bce38-106">本教學課程介紹 [服務摘要] 刀鋒視窗、說明儀表板內容和功能，並描述您可以從這個頁面執行的工作。</span><span class="sxs-lookup"><span data-stu-id="bce38-106">This tutorial introduces the service summary blade, explains the dashboard content and function, and describes the tasks that you can perform from this page.</span></span>

![服務摘要](./media/storsimple-8000-service-dashboard/service-summary1.png)


## <a name="management-commands"></a><span data-ttu-id="bce38-108">管理命令</span><span class="sxs-lookup"><span data-stu-id="bce38-108">Management commands</span></span>

<span data-ttu-id="bce38-109">在 StorSimple 的 [服務摘要] 刀鋒視窗中，您會看到可用來管理 StorSimple 裝置管理員服務，以及已向此服務註冊的 StorSimple 8000 系列裝置的選項。</span><span class="sxs-lookup"><span data-stu-id="bce38-109">In the StorSimple service summary blade, you see the options for managing your StorSimple Device Manager service and the StorSimple 8000 series devices registered to this service.</span></span> <span data-ttu-id="bce38-110">您在刀鋒視窗的上方橫幅和左邊會看到管理命令。</span><span class="sxs-lookup"><span data-stu-id="bce38-110">You see the management commands across the top of the blade and on the left side.</span></span>

![命令列](./media/storsimple-8000-service-dashboard/service-summary2.png)

<span data-ttu-id="bce38-112">使用這些選項來執行各種作業，例如新增共用或磁碟區，或監視 StorSimple 裝置上執行的各種作業。</span><span class="sxs-lookup"><span data-stu-id="bce38-112">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the StorSimple devices.</span></span>


## <a name="essentials"></a><span data-ttu-id="bce38-113">基本資訊</span><span class="sxs-lookup"><span data-stu-id="bce38-113">Essentials</span></span>

<span data-ttu-id="bce38-114">基本資訊區域擷取一些重要屬性，例如原本建立 StorSimple 裝置管理員的資源群組、位置和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bce38-114">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

![基本資訊](./media/storsimple-8000-service-dashboard/service-summary3.png)

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="bce38-116">StorSimple 裝置管理員服務摘要</span><span class="sxs-lookup"><span data-stu-id="bce38-116">StorSimple Device Manager service summary</span></span>

* <span data-ttu-id="bce38-117">[警示] 圖格提供所有裝置上之所有作用中警示的快照集 (依警示嚴重性分組)。</span><span class="sxs-lookup"><span data-stu-id="bce38-117">The **Alerts** tile provides a snapshot of all the active alerts across all devices, grouped by alert severity.</span></span>

    ![[警示] 圖格](./media/storsimple-8000-service-dashboard/service-summary4.png)

    <span data-ttu-id="bce38-119">按一下此圖格來開啟 [警示] 刀鋒視窗，您可以在其中按一下個別警示來檢視該警示的其他詳細資料，包括任何建議的動作。</span><span class="sxs-lookup"><span data-stu-id="bce38-119">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="bce38-120">如果已解決問題，您也可以清除警示。</span><span class="sxs-lookup"><span data-stu-id="bce38-120">You can also clear the alert if the issue has been resolved.</span></span>

    ![按一下 [警示] 圖格](./media/storsimple-8000-service-dashboard/service-summary8.png)

* <span data-ttu-id="bce38-122">[容量] 圖格顯示所有裝置上的已佈建和剩餘主要儲存空間 (相對於所有裝置上的可用總儲存空間)。</span><span class="sxs-lookup"><span data-stu-id="bce38-122">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all devices relative to the total storage available across all devices.</span></span> <span data-ttu-id="bce38-123">[已佈建] 是指已備妥和配置供使用的儲存空間數量，[剩餘] 是指所有裝置上可佈建的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="bce38-123">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all devices.</span></span>

    ![[容量] 圖格](./media/storsimple-8000-service-dashboard/service-summary6.png)

    <span data-ttu-id="bce38-125">[剩餘階層式] 容量是包括雲端的可供佈建容量，而 [剩餘本機] 是連接至 StorSimple 8000 系列裝置之磁碟上的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="bce38-125">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the StorSimple 8000 series devices.</span></span>


* <span data-ttu-id="bce38-126">在 [使用量] 圖表中，您可以查看裝置的相關度量。</span><span class="sxs-lookup"><span data-stu-id="bce38-126">In the **Usage** chart, you can see the relevant metrics for your devices.</span></span> <span data-ttu-id="bce38-127">您可以檢視所有裝置上已使用的主要儲存空間，以及裝置在過去 7 天 (預設期間) 所耗用的雲端儲存空間。</span><span class="sxs-lookup"><span data-stu-id="bce38-127">You can view the primary storage used across all devices, and the cloud storage consumed by devices over the past 7 days, the default time period.</span></span> 

    ![使用量圖格](./media/storsimple-8000-service-dashboard/service-summary7.png) 

    <span data-ttu-id="bce38-129">若要選擇不同的時間間隔，請使用圖表右上角的 [編輯] 選項。</span><span class="sxs-lookup"><span data-stu-id="bce38-129">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![按一下 [使用量] 圖格](./media/storsimple-8000-service-dashboard/service-summary10.png)

     ![匯出圖表資料](./media/storsimple-8000-service-dashboard/service-summary11.png)

* <span data-ttu-id="bce38-132">[裝置] 圖格提供 StorSimple 裝置管理員中 StorSimple 8000 系列裝置的數目摘要 (依裝置狀態分組)。</span><span class="sxs-lookup"><span data-stu-id="bce38-132">The **Devices** tile provides a summary of the number of StorSimple 8000 series devices in your StorSimple Device Manager grouped by device status.</span></span> 

    ![[裝置] 圖格](./media/storsimple-8000-service-dashboard/service-summary5.png)

    <span data-ttu-id="bce38-134">按一下此圖格以開啟 [裝置] 清單刀鋒視窗，然後按一下個別裝置來深入該裝置的裝置摘要。</span><span class="sxs-lookup"><span data-stu-id="bce38-134">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="bce38-135">您也可以從指定的裝置摘要刀鋒視窗執行裝置特定的動作。</span><span class="sxs-lookup"><span data-stu-id="bce38-135">You can also perform device-specific actions from a given device summary blade.</span></span> <span data-ttu-id="bce38-136">如需裝置摘要刀鋒視窗的詳細資訊，請參閱[裝置摘要刀鋒視窗](storsimple-8000-device-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="bce38-136">For more information about the device summary blade, go to [Device summary blade](storsimple-8000-device-dashboard.md).</span></span>

    ![按一下 [裝置] 圖格](./media/storsimple-8000-service-dashboard/service-summary9.png)

## <a name="view-the-activity-logs"></a><span data-ttu-id="bce38-138">檢視活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="bce38-138">View the activity logs</span></span>

<span data-ttu-id="bce38-139">若要檢視 StorSimple 裝置管理員中執行的各種作業，請按一下 StorSimple 服務摘要刀鋒視窗左側的 [活動記錄檔] 連結。</span><span class="sxs-lookup"><span data-stu-id="bce38-139">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="bce38-140">這會帶您前往 [活動記錄檔] 刀鋒視窗，您可以在其中看到最近執行的作業摘要。</span><span class="sxs-lookup"><span data-stu-id="bce38-140">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![活動記錄檔](./media/storsimple-8000-service-dashboard/activity-logs1.png)
## <a name="next-steps"></a><span data-ttu-id="bce38-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bce38-142">Next steps</span></span>

* <span data-ttu-id="bce38-143">深入了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-8000-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="bce38-143">Learn more about how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

