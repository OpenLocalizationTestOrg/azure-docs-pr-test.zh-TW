---
title: "使用 StorSimple Manager 裝置儀表板 | Microsoft Docs"
description: "描述 StorSimple Manager 服務裝置儀表板，以及如何用它來檢視儲存體度量和連線的啟動器，並尋找序號和 IQN。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d8035b9608ca3bac3d4822c7c755b81c96d481e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-dashboard-in-storsimple-manager-service"></a><span data-ttu-id="a61a0-103">在 StorSimple Manager 服務中使用裝置儀表板</span><span class="sxs-lookup"><span data-stu-id="a61a0-103">Use the device dashboard in StorSimple Manager service</span></span>  

## <a name="overview"></a><span data-ttu-id="a61a0-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a61a0-104">Overview</span></span>
<span data-ttu-id="a61a0-105">StorSimple Manager 裝置儀表板可提供特定 StorSimple 裝置的資訊概觀；相對於服務儀表板，其提供 Microsoft Azure StorSimple 解決方案中所有裝置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a61a0-105">The StorSimple Manager device dashboard gives you an overview of information for a specific  StorSimple device, in contrast to the service dashboard, which gives you information about all of the devices included in your Microsoft Azure StorSimple solution.</span></span>

![裝置儀表板頁面](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

<span data-ttu-id="a61a0-107">儀表板包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="a61a0-107">The dashboard contains the following information:</span></span>

* <span data-ttu-id="a61a0-108">**圖表區域** – 您可以在儀表板頂端的圖表區域中查看相關儲存體度量。</span><span class="sxs-lookup"><span data-stu-id="a61a0-108">**Chart area** – You can see the relevant storage metrics in the chart area at the top of the dashboard.</span></span> <span data-ttu-id="a61a0-109">在此圖表中，您可以檢視主要儲存體總計 (主機寫入至您的裝置的資料數量) 和您的裝置一段時間內所使用的雲端儲存體總計的度量資訊。</span><span class="sxs-lookup"><span data-stu-id="a61a0-109">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="a61a0-110">在此情況下，「主要儲存體」是指由主機寫入的資料總量，並可依磁碟區類型細分︰「主要分層式儲存體」包含在本機儲存的資料和分層至雲端的資料；「主要本機釘選儲存體」只包含在本機儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="a61a0-110">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud; *primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="a61a0-111">相反地，「雲端儲存體」是儲存在雲端中的資料總量測量。</span><span class="sxs-lookup"><span data-stu-id="a61a0-111">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="a61a0-112">這包括分層式資料和備份。</span><span class="sxs-lookup"><span data-stu-id="a61a0-112">This includes tiered data and backups.</span></span> <span data-ttu-id="a61a0-113">請注意，儲存在雲端中的資料會進行重複資料刪除和壓縮，而主要儲存體會指出進行重複資料刪除和壓縮之前已使用的儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="a61a0-113">Note that data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="a61a0-114">(您可以比較這兩個數字以了解壓縮率)。對於主要和雲端儲存體，所顯示的數量會以您設定的追蹤頻率為基礎。</span><span class="sxs-lookup"><span data-stu-id="a61a0-114">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown will be based on the tracking frequency you configure.</span></span> <span data-ttu-id="a61a0-115">例如，如果您選擇一週頻率，則此圖表會顯示上週每一天的資料。</span><span class="sxs-lookup"><span data-stu-id="a61a0-115">For example, if you choose a one week frequency, then the chart will show data for each day in the previous week.</span></span>
  
     <span data-ttu-id="a61a0-116">您可以如下所示設定圖表：</span><span class="sxs-lookup"><span data-stu-id="a61a0-116">You can configure the chart as follows:</span></span>
  
  * <span data-ttu-id="a61a0-117">若要查看一段時間耗用的雲端儲存體數量，請選取 [ **使用的雲端儲存體** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="a61a0-117">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="a61a0-118">若要查看主機所寫入的儲存體總量，請選取 [使用的主要分層式儲存體] 和 [使用的本機釘選儲存體] 選項。</span><span class="sxs-lookup"><span data-stu-id="a61a0-118">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> <span data-ttu-id="a61a0-119">在圖中，兩個選項都已選取；因此，此圖表會顯示雲端和主要儲存體的儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="a61a0-119">In the illustration, both options are selected; therefore, the chart shows storage amounts for both cloud and primary storage.</span></span> <span data-ttu-id="a61a0-120">請注意，任何在安裝 Update 2 之前使用的主要儲存體皆是以「使用的主要分層式儲存體」  行表示。</span><span class="sxs-lookup"><span data-stu-id="a61a0-120">Note that any primary storage used prior to installing Update 2 is represented by the **PRIMARY TIERED STORAGE USED** line.</span></span>
  * <span data-ttu-id="a61a0-121">使用圖表右上角的下拉式功能表，指定 1 週、1 個月、3 個月或 1 年的期間。</span><span class="sxs-lookup"><span data-stu-id="a61a0-121">Use the drop-down menu in the top-right corner of the chart to specify a 1-week, 1-month, 3-month, or 1-year time period.</span></span> <span data-ttu-id="a61a0-122">請注意，最上層圖表每天只會重新整理一次，因此會反映前一天的總計。</span><span class="sxs-lookup"><span data-stu-id="a61a0-122">Note that the top-level chart is refreshed only one time per day, and therefore will reflect the previous day's totals.</span></span>
    
    <span data-ttu-id="a61a0-123">如需詳細資訊，請參閱 [使用 StorSimple Manager 服務監視 StorSimple 裝置](storsimple-monitor-device.md)。</span><span class="sxs-lookup"><span data-stu-id="a61a0-123">For more information, see [Use the StorSimple Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>
* <span data-ttu-id="a61a0-124">**使用量概觀** – 在 [使用量概觀] 區域中，您可以看到使用的主要儲存體數量、佈建的儲存體數量以及您裝置的最大儲存體容量。</span><span class="sxs-lookup"><span data-stu-id="a61a0-124">**Usage overview** – In the **usage overview** area, you can see the amount of primary storage used, the amount of provisioned storage, and the maximum storage capacity for your device.</span></span> <span data-ttu-id="a61a0-125">藉由比較這些使用量數字與可用的最大儲存體數量，您可以快速查看是否需要取得額外的儲存體。</span><span class="sxs-lookup"><span data-stu-id="a61a0-125">By comparing these usage numbers to the maximum amount of storage that is available, you can see at a glance if you need to obtain additional storage.</span></span> <span data-ttu-id="a61a0-126">請注意，本概觀會每 15 分鐘更新一次，但由於更新頻率的差異，可能會顯示與上述圖表區域 (每日更新) 中不同的數字。</span><span class="sxs-lookup"><span data-stu-id="a61a0-126">Note that this overview is updated every 15 minutes and, because of the difference in update frequency, may show different numbers than those shown in the chart area above, which is updated daily.</span></span> <span data-ttu-id="a61a0-127">如需詳細資訊，請參閱 [使用 StorSimple Manager 服務監視 StorSimple 裝置](storsimple-monitor-device.md)。</span><span class="sxs-lookup"><span data-stu-id="a61a0-127">For more information, see [Use the StorSimple Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>
* <span data-ttu-id="a61a0-128">**警示** – [警示] 區域包含您裝置的警示概觀。</span><span class="sxs-lookup"><span data-stu-id="a61a0-128">**Alerts** – The **alerts** area contains an overview of the alerts for your device.</span></span> <span data-ttu-id="a61a0-129">警示會依嚴重性分組，並提供一個計數以顯示每個嚴重性層級的警示數目。</span><span class="sxs-lookup"><span data-stu-id="a61a0-129">Alerts are grouped by severity, and a count is provided of the number of alerts at each severity level.</span></span> <span data-ttu-id="a61a0-130">按一下警示嚴重性即可開啟 [警示] 索引標籤的限定範圍檢視，僅顯示此裝置的該嚴重性層級的警示。</span><span class="sxs-lookup"><span data-stu-id="a61a0-130">Clicking the alert severity opens a scoped view of the alerts tab to show you only the alerts of that severity level for this device.</span></span>
* <span data-ttu-id="a61a0-131">**工作** – [工作] 區域會顯示最近工作活動的結果。</span><span class="sxs-lookup"><span data-stu-id="a61a0-131">**Jobs** – The **jobs** area shows you the outcome of recent job activity.</span></span> <span data-ttu-id="a61a0-132">這可確保系統如預期般運作，或可讓您知道您需要採取更正動作。</span><span class="sxs-lookup"><span data-stu-id="a61a0-132">This can assure you that the system is operating as expected, or it can let you know that you need to take corrective action.</span></span> <span data-ttu-id="a61a0-133">若要查看最近完成工作的詳細資訊，請按一下 [在過去 24 小時內成功的工作] 。</span><span class="sxs-lookup"><span data-stu-id="a61a0-133">To see more information about recently completed jobs, click **Jobs succeeded in the last 24 hours**.</span></span>
* <span data-ttu-id="a61a0-134">儀表板右邊的 [快速概覽]  區域提供實用資訊，例如裝置機型、序號、狀態、描述和磁碟區數目。</span><span class="sxs-lookup"><span data-stu-id="a61a0-134">The **quick glance** area on the right of the dashboard provides useful information such as device model, serial number, status, description, and number of volumes.</span></span>

<span data-ttu-id="a61a0-135">您也可以從裝置儀表板設定容錯移轉及檢視連接的啟動器。</span><span class="sxs-lookup"><span data-stu-id="a61a0-135">You can also configure failover and view connected initiators from the device dashboard.</span></span>

<span data-ttu-id="a61a0-136">可在此頁面執行的一般工作包括：</span><span class="sxs-lookup"><span data-stu-id="a61a0-136">The common tasks that can be performed on this page are:</span></span>

* <span data-ttu-id="a61a0-137">檢視連接的啟動器</span><span class="sxs-lookup"><span data-stu-id="a61a0-137">View connected initiators</span></span>
* <span data-ttu-id="a61a0-138">尋找裝置序號</span><span class="sxs-lookup"><span data-stu-id="a61a0-138">Find the device serial number</span></span>
* <span data-ttu-id="a61a0-139">尋找裝置目標 IQN</span><span class="sxs-lookup"><span data-stu-id="a61a0-139">Find the device target IQN</span></span>

## <a name="view-connected-initiators"></a><span data-ttu-id="a61a0-140">檢視連接的啟動器</span><span class="sxs-lookup"><span data-stu-id="a61a0-140">View connected initiators</span></span>
<span data-ttu-id="a61a0-141">按一下裝置儀表板的 [快速概覽] 區域中提供的 [檢視連線的啟動器] 連結，即可檢視連接至您裝置的 iSCSI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="a61a0-141">You can view the iSCSI initiators that are connected to your device by clicking the **View connected initiators** link provided in the **quick glance** area of your device dashboard.</span></span> <span data-ttu-id="a61a0-142">此頁面提供已成功連接到您的裝置之啟動器的表格式清單。</span><span class="sxs-lookup"><span data-stu-id="a61a0-142">This page provides a tabular listing of the initiators that have successfully connected to your device.</span></span> <span data-ttu-id="a61a0-143">對於每個啟動器，您可以查看：</span><span class="sxs-lookup"><span data-stu-id="a61a0-143">For each initiator, you can see:</span></span>

* <span data-ttu-id="a61a0-144">已連接之啟動器的 iSCSI 完整格式名稱 (IQN)。</span><span class="sxs-lookup"><span data-stu-id="a61a0-144">The iSCSI Qualified Name (IQN) of the connected initiator.</span></span>
* <span data-ttu-id="a61a0-145">允許這個已連接之啟動器的存取控制記錄 (ACR) 名稱。</span><span class="sxs-lookup"><span data-stu-id="a61a0-145">The name of the access control record (ACR) that allows this connected initiator.</span></span>
* <span data-ttu-id="a61a0-146">已連接之啟動器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a61a0-146">The IP address of the connected initiator.</span></span>
* <span data-ttu-id="a61a0-147">您的存放裝置上啟動器連接到的網路介面。</span><span class="sxs-lookup"><span data-stu-id="a61a0-147">The network interfaces that the initiator is connected to on your storage device.</span></span> <span data-ttu-id="a61a0-148">範圍從 DATA 0 到 DATA 5。</span><span class="sxs-lookup"><span data-stu-id="a61a0-148">These can range from DATA 0 to DATA 5.</span></span>
* <span data-ttu-id="a61a0-149">根據目前的 ACR 組態，連接的啟動器允許存取的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a61a0-149">All the volumes that the connected initiator is allowed to access according to the current ACR configuration.</span></span>

<span data-ttu-id="a61a0-150">如果您在此清單中看到非預期的啟動器，或看不到預期的啟動器，請檢閱您的 ACR 組態。</span><span class="sxs-lookup"><span data-stu-id="a61a0-150">If you see unexpected initiators in this list or do not see the expected ones, review your ACR configuration.</span></span> <span data-ttu-id="a61a0-151">最多 512 個啟動器可連接到您的裝置。</span><span class="sxs-lookup"><span data-stu-id="a61a0-151">A maximum of 512 initiators can connect to your device.</span></span>

## <a name="find-the-device-serial-number"></a><span data-ttu-id="a61a0-152">尋找裝置序號</span><span class="sxs-lookup"><span data-stu-id="a61a0-152">Find the device serial number</span></span>
<span data-ttu-id="a61a0-153">當您在裝置上設定 Microsoft 多重路徑 I/O (MPIO) 時，您可能需要裝置序號。</span><span class="sxs-lookup"><span data-stu-id="a61a0-153">You may need the device serial number when you configure Microsoft Multipath I/O (MPIO) on the device.</span></span> <span data-ttu-id="a61a0-154">執行下列步驟來尋找裝置序號。</span><span class="sxs-lookup"><span data-stu-id="a61a0-154">Perform the following steps to find the device serial number.</span></span>

#### <a name="to-find-the-device-serial-number"></a><span data-ttu-id="a61a0-155">若要尋找裝置序號：</span><span class="sxs-lookup"><span data-stu-id="a61a0-155">To find the device serial number</span></span>
1. <span data-ttu-id="a61a0-156">瀏覽至 [裝置] > [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="a61a0-156">Navigate to **Devices** > **Dashboard**.</span></span>
2. <span data-ttu-id="a61a0-157">在儀表板的右窗格中，找出 [快速概覽]  區域。</span><span class="sxs-lookup"><span data-stu-id="a61a0-157">In the right pane of the dashboard, locate the **quick glance** area.</span></span>
3. <span data-ttu-id="a61a0-158">向下捲動並找出序號。</span><span class="sxs-lookup"><span data-stu-id="a61a0-158">Scroll down and locate the serial number.</span></span>

## <a name="find-the-device-target-iqn"></a><span data-ttu-id="a61a0-159">尋找裝置目標 IQN</span><span class="sxs-lookup"><span data-stu-id="a61a0-159">Find the device target IQN</span></span>
<span data-ttu-id="a61a0-160">當您在 StorSimple 裝置上設定 Challenge Handshake 驗證通訊協定 (CHAP) 時，您可能需要裝置目標 IQN。</span><span class="sxs-lookup"><span data-stu-id="a61a0-160">You may need the device target IQN when you configure the Challenge Handshake Authentication Protocol (CHAP) on your StorSimple device.</span></span> <span data-ttu-id="a61a0-161">執行下列步驟來尋找裝置目標 IQN。</span><span class="sxs-lookup"><span data-stu-id="a61a0-161">Perform the following steps to find the device target IQN.</span></span>

### <a name="to-find-the-device-target-iqn"></a><span data-ttu-id="a61a0-162">若要尋找裝置目標 IQN：</span><span class="sxs-lookup"><span data-stu-id="a61a0-162">To find the device target IQN</span></span>
1. <span data-ttu-id="a61a0-163">瀏覽至 [裝置] > [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="a61a0-163">Navigate to **Devices** > **Dashboard**.</span></span>
2. <span data-ttu-id="a61a0-164">在儀表板的右窗格中，找出 [快速概覽]  區域。</span><span class="sxs-lookup"><span data-stu-id="a61a0-164">In the right pane of the dashboard, locate the **quick glance** area.</span></span>
3. <span data-ttu-id="a61a0-165">向下捲動並找出目標 IQN。</span><span class="sxs-lookup"><span data-stu-id="a61a0-165">Scroll down and locate the target IQN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a61a0-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a61a0-166">Next steps</span></span>
* <span data-ttu-id="a61a0-167">[深入了解 StorSimple Manager 服務儀表板](storsimple-service-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="a61a0-167">Learn more about the [StorSimple Manager service dashboard](storsimple-service-dashboard.md).</span></span>
* <span data-ttu-id="a61a0-168">深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="a61a0-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

