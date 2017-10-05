---
title: "StorSimple Virtual Array 服務摘要刀鋒視窗 | Microsoft Docs"
description: "描述 StorSimple 裝置管理員的服務摘要刀鋒視窗，並說明如何使用它來監視 StorSimple Virtual Array 的健康狀態。"
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 8a2b9a84-b0e6-48b9-b366-d16f004241a5
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 284e404c44505a98d9e0ed5abe87cd945415af56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-summary-blade-for-storsimple-device-manager-connected-to-storsimple-virtual-array"></a><span data-ttu-id="c47e6-103">在連接至 Microsoft Azure StorSimple Virtual Array 的 StorSimple 裝置管理員中使用服務摘要刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="c47e6-103">Use the service summary blade for StorSimple Device Manager connected to StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="c47e6-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c47e6-104">Overview</span></span>
<span data-ttu-id="c47e6-105">針對連接至服務的 StorSimple Virtual Array (也稱為 StorSimple 內部部署虛擬裝置，或簡稱虛擬裝置)，StorSimple 裝置管理員的服務摘要刀鋒視窗提供摘要檢視，並醒目提示需要系統管理員注意的裝置。</span><span class="sxs-lookup"><span data-stu-id="c47e6-105">The service summary blade for the StorSimple Device Manager provides a summary view of the StorSimple Virtual Arrays (also known as StorSimple on-premises virtual devices or virtual devices) that are connected to your service, highlighting those that need a system administrator's attention.</span></span> <span data-ttu-id="c47e6-106">本教學課程介紹服務摘要刀鋒視窗、說明內容和功能，並描述您可以從這個刀鋒視窗執行的工作。</span><span class="sxs-lookup"><span data-stu-id="c47e6-106">This tutorial introduces the service summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

![服務儀表板](./media/storsimple-virtual-array-service-summary/service-blade.png)

## <a name="management-commands-and-essentials"></a><span data-ttu-id="c47e6-108">管理命令和基本資訊</span><span class="sxs-lookup"><span data-stu-id="c47e6-108">Management commands and essentials</span></span>
<span data-ttu-id="c47e6-109">在 StorSimple 摘要刀鋒視窗中，您會看到選項可用來管理 StorSimple 裝置管理員服務，以及已向此服務註冊的虛擬陣列。</span><span class="sxs-lookup"><span data-stu-id="c47e6-109">In the StorSimple summary blade, you see the options for managing your StorSimple Device Manager service as well as the virtual arrays registered to this service.</span></span> <span data-ttu-id="c47e6-110">您在刀鋒視窗的上方橫幅和左邊會看到管理命令。</span><span class="sxs-lookup"><span data-stu-id="c47e6-110">You see the management commands across the top of the blade and on the left side.</span></span>

<span data-ttu-id="c47e6-111">請使用這些選項來執行各種作業，例如新增共用或磁碟區，或監視虛擬陣列上執行的各種作業。</span><span class="sxs-lookup"><span data-stu-id="c47e6-111">Use these options to perform various operations such as add shares or volumes, or monitor the various jobs running on the virtual arrays.</span></span>

<span data-ttu-id="c47e6-112">基本資訊區域擷取一些重要屬性，例如原本建立 StorSimple 裝置管理員的資源群組、位置和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c47e6-112">The essentials area captures some of the important properties such as, the resource group, location, and subscription in which your StorSimple Device Manager was created.</span></span>

## <a name="storsimple-device-manager-service-summary"></a><span data-ttu-id="c47e6-113">StorSimple 裝置管理員服務摘要</span><span class="sxs-lookup"><span data-stu-id="c47e6-113">StorSimple Device Manager service summary</span></span>
* <span data-ttu-id="c47e6-114">[警示] 圖格提供所有虛擬裝置上的所有作用中警示的快照集，依警示嚴重性分組。</span><span class="sxs-lookup"><span data-stu-id="c47e6-114">The **Alerts** tile provides a snapshot of all the active alerts across all virtual devices, grouped by alert severity.</span></span> <span data-ttu-id="c47e6-115">按一下此圖格來開啟 [警示] 刀鋒視窗，您可以在其中按一下個別警示來檢視該警示的其他詳細資料，包括任何建議的動作。</span><span class="sxs-lookup"><span data-stu-id="c47e6-115">Clicking the tile opens the **Alerts** blade, where you can click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="c47e6-116">如果已解決問題，您也可以清除警示。</span><span class="sxs-lookup"><span data-stu-id="c47e6-116">You can also clear the alert if the issue has been resolved.</span></span>
* <span data-ttu-id="c47e6-117">[容量] 圖格顯示所有虛擬裝置上相對於可用的總儲存空間而言，已佈建和剩餘的主要儲存空間。</span><span class="sxs-lookup"><span data-stu-id="c47e6-117">The **Capacity** tile displays shows the primary storage that is provisioned and remaining across all virtual devices relative to the total storage available across all virtual devices.</span></span> <span data-ttu-id="c47e6-118">[已佈建] 是指已備妥和配置供使用的儲存空間數量，[剩餘] 是指所有虛擬裝置上可佈建的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="c47e6-118">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across all virtual devices.</span></span> <span data-ttu-id="c47e6-119">[剩餘階層式] 容量是可供佈建的容量，包括雲端，而 [剩餘本機] 是連接至虛擬陣列的磁碟上剩餘的容量。</span><span class="sxs-lookup"><span data-stu-id="c47e6-119">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to the virtual arrays.</span></span>
* <span data-ttu-id="c47e6-120">在 [使用量] 圖表中，您可以查看虛擬裝置的相關度量。</span><span class="sxs-lookup"><span data-stu-id="c47e6-120">In the **Usage** chart, you can see the relevant metrics for your virtual devices.</span></span> <span data-ttu-id="c47e6-121">您可以檢視所有虛擬裝置已使用的主要儲存空間，以及虛擬裝置在過去 7 天 (預設期間) 耗用的雲端儲存空間。</span><span class="sxs-lookup"><span data-stu-id="c47e6-121">You can view the primary storage used across all virtual devices, as well as the cloud storage consumed by virtual devices over the past 7 days, the default time period.</span></span> <span data-ttu-id="c47e6-122">使用圖表右上角的 [編輯] 選項來選擇不同的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="c47e6-122">Use the **Edit** option in the top-right corner of the chart to choose a different time scale.</span></span>
* <span data-ttu-id="c47e6-123">[裝置] 圖格提供 StorSimple 裝置管理員中的虛擬陣列數目摘要 (依裝置狀態分組)。</span><span class="sxs-lookup"><span data-stu-id="c47e6-123">The **Devices** tile provides a summary of the number of virtual arrays in your StorSimple Device Manager grouped by device status.</span></span> <span data-ttu-id="c47e6-124">按一下此圖格以開啟 [裝置] 清單刀鋒視窗，然後按一下個別裝置來深入該裝置的裝置摘要。</span><span class="sxs-lookup"><span data-stu-id="c47e6-124">Click this tile to open the **Devices** list blade and then click an individual device to drill into the device summary specific to the device.</span></span> <span data-ttu-id="c47e6-125">您也可以從指定的裝置摘要刀鋒視窗執行裝置的特定動作。</span><span class="sxs-lookup"><span data-stu-id="c47e6-125">You can also perform device specific actions from a given device summary blade.</span></span> <span data-ttu-id="c47e6-126">如需裝置摘要刀鋒視窗的詳細資訊，請參閱[裝置摘要刀鋒視窗](storsimple-virtual-array-device-summary.md)。</span><span class="sxs-lookup"><span data-stu-id="c47e6-126">For more information about the device summary blade, go to [Device summary blade](storsimple-virtual-array-device-summary.md).</span></span>

## <a name="view-the-activity-logs"></a><span data-ttu-id="c47e6-127">檢視活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="c47e6-127">View the activity logs</span></span>
<span data-ttu-id="c47e6-128">若要檢視 StorSimple 裝置管理員中執行的各種作業，請按一下 StorSimple 服務摘要刀鋒視窗左側的 [活動記錄檔] 連結。</span><span class="sxs-lookup"><span data-stu-id="c47e6-128">To view the various operations carried out within your StorSimple Device Manager, click the **Activity logs** link on the left side of your StorSimple service summary blade.</span></span> <span data-ttu-id="c47e6-129">這會帶您前往 [活動記錄檔] 刀鋒視窗，您可以在其中看到最近執行的作業摘要。</span><span class="sxs-lookup"><span data-stu-id="c47e6-129">This takes you to the **Activity logs** blade, where you can see a summary of the recent operations carried out.</span></span>

![活動記錄檔](./media/storsimple-virtual-array-service-summary/activity-log.png)

## <a name="next-steps"></a><span data-ttu-id="c47e6-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c47e6-131">Next steps</span></span>
<span data-ttu-id="c47e6-132">了解如何 [使用本機 Web UI 來管理 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。</span><span class="sxs-lookup"><span data-stu-id="c47e6-132">Learn how to [use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

