---
title: "StorSimple Virtual Array 裝置摘要刀鋒視窗 | Microsoft Docs"
description: "描述 StorSimple 裝置管理員的裝置摘要刀鋒視窗，並說明如何使用它來監視 StorSimple Virtual Array 的健康狀態。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 35413d597c3b6b1c7600241a78572b63f982d175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="11821-103">在連接至 Microsoft Azure StorSimple Virtual Array 的 StorSimple 裝置管理員中使用裝置摘要刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="11821-103">Use the device summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="11821-104">概觀</span><span class="sxs-lookup"><span data-stu-id="11821-104">Overview</span></span>

<span data-ttu-id="11821-105">對於已向給定 StorSimple 裝置管理員註冊的 StorSimple Virtual Array，StorSimple 裝置管理員的裝置刀鋒視窗提供摘要檢視，並醒目提示需要系統管理員注意的裝置問題。</span><span class="sxs-lookup"><span data-stu-id="11821-105">The StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="11821-106">本教學課程介紹裝置摘要刀鋒視窗、說明內容和功能，並描述您可以從這個刀鋒視窗執行的工作。</span><span class="sxs-lookup"><span data-stu-id="11821-106">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="11821-107">裝置摘要刀鋒視窗會顯示以下資訊：</span><span class="sxs-lookup"><span data-stu-id="11821-107">The device summary blade displays the following information:</span></span>

![裝置儀表板](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="11821-109">管理</span><span class="sxs-lookup"><span data-stu-id="11821-109">Management</span></span>

<span data-ttu-id="11821-110">在 StorSimple 裝置刀鋒視窗中，您會看到 StorSimple 裝置的管理選項。</span><span class="sxs-lookup"><span data-stu-id="11821-110">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="11821-111">您在刀鋒視窗的上方橫幅和左邊會看到管理命令。</span><span class="sxs-lookup"><span data-stu-id="11821-111">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="11821-112">請使用這些選項來新增共用或磁碟區，或是更新或容錯移轉虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="11821-112">Use these options to add shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="11821-113">基本資訊區域擷取一些重要屬性，例如陣列的狀態、模型、軟體版本及 **Web UI** 的連結。</span><span class="sxs-lookup"><span data-stu-id="11821-113">The essentials area captures some of the important properties such as, the status, model, software version as well as a link to the **Web UI** of the array.</span></span> <span data-ttu-id="11821-114">如果您在內部網路，您可以直接啟動[本機 Web UI](storsimple-ova-web-ui-admin.md) 來管理虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="11821-114">If you are on an internal network, you can directly launch the [local web UI](storsimple-ova-web-ui-admin.md) to administer your virtual array.</span></span>

![裝置的基本資訊](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="11821-116">StorSimple 裝置摘要</span><span class="sxs-lookup"><span data-stu-id="11821-116">StorSimple device summary</span></span>

* <span data-ttu-id="11821-117">[警示] 圖格提供虛擬陣列之所有作用中警示的快照集 (依警示嚴重性分組)。</span><span class="sxs-lookup"><span data-stu-id="11821-117">The **Alerts** tile provides a snapshot of all the active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="11821-118">按一下此圖格來開啟 [警示] 刀鋒視窗，然後按一下個別警示來檢視該警示的其他詳細資料，包括任何建議的動作。</span><span class="sxs-lookup"><span data-stu-id="11821-118">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="11821-119">如果已解決問題，您也可以清除警示。</span><span class="sxs-lookup"><span data-stu-id="11821-119">You can also clear the alert if the issue has been resolved.</span></span>

* <span data-ttu-id="11821-120">[容量] 圖格顯示虛擬裝置上相對於可用的總儲存空間而言，已佈建和剩餘的主要儲存空間。</span><span class="sxs-lookup"><span data-stu-id="11821-120">The **Capacity** tile displays the primary storage that is provisioned and remaining across the virtual device relative to the total storage available for the same.</span></span> <span data-ttu-id="11821-121">[已佈建] 是指已備妥和配置供使用的儲存空間數量，[剩餘] 是指這個裝置上可佈建的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="11821-121">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="11821-122">[剩餘階層式] 容量是可供佈建的容量，包括雲端，而 [剩餘本機] 是連接至此虛擬陣列的磁碟上剩餘的容量。</span><span class="sxs-lookup"><span data-stu-id="11821-122">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this virtual array.</span></span>

* <span data-ttu-id="11821-123">在 [使用量] 圖表中，您可以檢視整個虛擬陣列已使用的主要儲存空間，以及過去 7 天 (預設期間) 耗用的雲端儲存空間。</span><span class="sxs-lookup"><span data-stu-id="11821-123">In the **Usage** chart, you can view the primary storage used across your virtual array, as well as the cloud storage consumed  over the past 7 days, the default time period.</span></span> <span data-ttu-id="11821-124">使用圖表右上角的 [編輯] 選項來選擇不同的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="11821-124">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>

* <span data-ttu-id="11821-125">[共用] 或 [磁碟區] 圖格提供裝置中的共用或磁碟區數目的摘要 (依狀態分組)。</span><span class="sxs-lookup"><span data-stu-id="11821-125">The **Shares** or **Volumes** tile provides a summary of the number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="11821-126">按一下此圖格來開啟 [共用] 或 [磁碟區] 清單刀鋒視窗，然後按一下個別共用或磁碟區來檢視或修改其屬性。</span><span class="sxs-lookup"><span data-stu-id="11821-126">Click the tile to open the **Shares**  or **Volumes** list blade, and then click on an individual share or volume to view or modify its properties.</span></span> <span data-ttu-id="11821-127">如需詳細資訊，請參閱如何[管理共用](storsimple-virtual-array-manage-shares.md)或[管理磁碟區](storsimple-virtual-array-manage-volumes.md)。</span><span class="sxs-lookup"><span data-stu-id="11821-127">For more information, see how to [manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="11821-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11821-128">Next steps</span></span>
<span data-ttu-id="11821-129">了解如何：</span><span class="sxs-lookup"><span data-stu-id="11821-129">Learn how to:</span></span>
- [<span data-ttu-id="11821-130">管理 StorSimple Virtual Array 上的共用</span><span class="sxs-lookup"><span data-stu-id="11821-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="11821-131">管理 StorSimple Virtual Array 上的磁碟區</span><span class="sxs-lookup"><span data-stu-id="11821-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

