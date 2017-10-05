---
title: "監視 StorSimple 裝置 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 服務來監視 I/O 效能、容量使用率、網路輸送量和裝置效能。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: bd4f7704-4f6f-47d0-927a-b1c91eabc453
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/16/2016
ms.author: alkohli
ms.openlocfilehash: d45bb37c8417785db0ea38be4375a998b6d9f109
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-monitor-your-storsimple-device"></a><span data-ttu-id="9e754-103">使用 StorSimple Manager 服務監視 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="9e754-103">Use the StorSimple Manager service to monitor your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="9e754-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9e754-104">Overview</span></span>
<span data-ttu-id="9e754-105">您可以使用 StorSimple Manager 服務來監視您的 StorSimple 解決方案中的特定裝置。</span><span class="sxs-lookup"><span data-stu-id="9e754-105">You can use the StorSimple Manager service to monitor specific devices within your StorSimple solution.</span></span> <span data-ttu-id="9e754-106">您可以根據 I/O 效能、容量使用率、網路輸送量，以及裝置效能計量建立自訂圖表。</span><span class="sxs-lookup"><span data-stu-id="9e754-106">You can create custom charts based on I/O performance, capacity utilization, network throughput, and device performance metrics.</span></span> 

<span data-ttu-id="9e754-107">若要檢視特定裝置的監視資訊，請在 Azure 傳統入口網站中，選取 [StorSimple Manager 服務]。</span><span class="sxs-lookup"><span data-stu-id="9e754-107">To view the monitoring information for a specific device, in the Azure classic portal, select the StorSimple Manager service.</span></span> <span data-ttu-id="9e754-108">按一下 [監視]  索引標籤，然後從裝置清單中選取。</span><span class="sxs-lookup"><span data-stu-id="9e754-108">Click the **Monitor** tab, and then select from the list of devices.</span></span> <span data-ttu-id="9e754-109">[監視]  頁面包含下列資訊。</span><span class="sxs-lookup"><span data-stu-id="9e754-109">The **Monitor** page contains the following information.</span></span>

## <a name="io-performance"></a><span data-ttu-id="9e754-110">I/O 效能</span><span class="sxs-lookup"><span data-stu-id="9e754-110">I/O performance</span></span>
<span data-ttu-id="9e754-111">**I/O 效能** 會追蹤與主機伺服器與裝置上的 iSCSI 啟動器介面之間，或裝置與雲端之間的讀取與寫入作業數目相關的計量。</span><span class="sxs-lookup"><span data-stu-id="9e754-111">**I/O performance** tracks metrics related to the number of read and write operations between either the iSCSI initiator interfaces on the host server and the device or the device and the cloud.</span></span> <span data-ttu-id="9e754-112">這項效能可以針對特定磁碟區、特定磁碟區容器，或所有磁碟區容器來測量。</span><span class="sxs-lookup"><span data-stu-id="9e754-112">This performance can be measured for a specific volume, a specific volume container, or all volume containers.</span></span>

<span data-ttu-id="9e754-113">下表顯示生產環境裝置之所有磁碟區中的裝置啟動器 I/O。</span><span class="sxs-lookup"><span data-stu-id="9e754-113">The chart below shows the I/O for the initiator to your device for all the volumes for a production device.</span></span> <span data-ttu-id="9e754-114">繪製的計量為每秒讀寫位元組大小、每秒讀寫 IO 作業，與讀寫延遲。</span><span class="sxs-lookup"><span data-stu-id="9e754-114">The metrics plotted are read and write bytes per second, read and write IO operations per second, and read and write latencies.</span></span>

![從啟動器到裝置的 IO 效能](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

<span data-ttu-id="9e754-116">就相同裝置而言，所繪製的 I/O 作業是針對所有磁碟區容器從裝置到雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="9e754-116">For the same device, the I/O operations are plotted for the data from the device to the cloud for all the volume containers.</span></span> <span data-ttu-id="9e754-117">在此裝置上，資料僅位於線性層內且並未溢出至雲端。</span><span class="sxs-lookup"><span data-stu-id="9e754-117">On this device, the data is only in the linear tier and nothing has spilled to the cloud.</span></span> <span data-ttu-id="9e754-118">從裝置到雲端並未發生讀寫作業。</span><span class="sxs-lookup"><span data-stu-id="9e754-118">There are no read-write operations occurring from device to the cloud.</span></span> <span data-ttu-id="9e754-119">因此，圖表中尖峰的間隔是 5 分鐘，這和裝置與服務之間的活動訊號檢查頻率對應。</span><span class="sxs-lookup"><span data-stu-id="9e754-119">Therefore, the peaks in the chart are at an interval of 5 minutes that corresponds to the frequency at which the heartbeat is checked between the device and the service.</span></span> 

![從裝置至雲端的 IO 效能](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

<span data-ttu-id="9e754-121">針對相同的裝置，磁碟區資料的雲端快照集從下午 2:00 開始建立。</span><span class="sxs-lookup"><span data-stu-id="9e754-121">For the same device, a cloud snapshot was taken for volume data starting at 2:00 pm.</span></span> <span data-ttu-id="9e754-122">這會導致資料從裝置流向雲端。</span><span class="sxs-lookup"><span data-stu-id="9e754-122">This resulted in data flowing from the device to the cloud.</span></span> <span data-ttu-id="9e754-123">在這段期間會提供雲端讀寫服務。</span><span class="sxs-lookup"><span data-stu-id="9e754-123">Reads-writes were served to the cloud in this duration.</span></span> <span data-ttu-id="9e754-124">IO 圖表會顯示建立快照集時各種計量中的尖峰所對應的時間。</span><span class="sxs-lookup"><span data-stu-id="9e754-124">The IO chart shows a peak in the various metrics corresponding to the time when the snapshot was taken.</span></span> 

![建立雲端快照集後至雲端的裝置 IO 效能](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a><span data-ttu-id="9e754-126">容量使用率</span><span class="sxs-lookup"><span data-stu-id="9e754-126">Capacity utilization</span></span>
<span data-ttu-id="9e754-127">**容量使用率** 會追蹤由磁碟區、磁碟區容器，或裝置所使用之資料儲存體空間數量的相關計量。</span><span class="sxs-lookup"><span data-stu-id="9e754-127">**Capacity utilization** tracks metrics related to the amount of data storage space that is used by the volumes, volume containers, or device.</span></span> <span data-ttu-id="9e754-128">您可以根據您的主要儲存體、雲端儲存體，或裝置儲存空間的容量使用率來建立報告。</span><span class="sxs-lookup"><span data-stu-id="9e754-128">You can create reports based on the capacity utilization of your primary storage, your cloud storage, or your device storage.</span></span> <span data-ttu-id="9e754-129">容量使用率可以在特定磁碟區、特定磁碟區容器，或所有磁碟區容器上測量。</span><span class="sxs-lookup"><span data-stu-id="9e754-129">Capacity utilization can be measured on a specific volume, a specific volume container, or all volume containers.</span></span>

<span data-ttu-id="9e754-130">主要、雲端及裝置儲存體容量的說明如下：</span><span class="sxs-lookup"><span data-stu-id="9e754-130">The primary, cloud, and device storage capacity can be described as follows:</span></span>

### <a name="primary-storage-capacity-utilization"></a><span data-ttu-id="9e754-131">主要儲存體容量使用率</span><span class="sxs-lookup"><span data-stu-id="9e754-131">Primary storage capacity utilization</span></span>
<span data-ttu-id="9e754-132">這些圖表顯示在進行重複資料刪除和壓縮之前寫入 StorSimple 磁碟區的資料量。</span><span class="sxs-lookup"><span data-stu-id="9e754-132">These charts show the amount of data written to StorSimple volumes before the data is deduplicated and compressed.</span></span> <span data-ttu-id="9e754-133">您可以檢視所有磁碟區或單一磁碟區的主要儲存體使用率。</span><span class="sxs-lookup"><span data-stu-id="9e754-133">You can view the primary storage utilization by all volumes or for a single volume.</span></span>

<span data-ttu-id="9e754-134">當您檢視所有磁碟區與每個個別磁碟區的主要儲存體磁碟區容量使用率圖表之比較，並將這兩種情況下的主要資料進行加總時，兩個數字之間可能會有不符。</span><span class="sxs-lookup"><span data-stu-id="9e754-134">When you view the primary storage volume capacity utilization charts for all volumes versus each of the individual volumes and sum up the primary data in both these cases, there may be a mismatch between the two numbers.</span></span> <span data-ttu-id="9e754-135">所有磁碟區上的主要資料總計可能與個別磁碟區的主要資料總和不相等。</span><span class="sxs-lookup"><span data-stu-id="9e754-135">The total primary data on all volumes may not add up to the sum total of the primary data of the individual volumes.</span></span> <span data-ttu-id="9e754-136">這可能是下列其中一個原因所造成：</span><span class="sxs-lookup"><span data-stu-id="9e754-136">This may be due to one of the following:</span></span>

* <span data-ttu-id="9e754-137">**所有磁碟區的資料包含快照資料**︰只有當您執行的版本是比 Update 3 舊的版本時，才會發生此行為。</span><span class="sxs-lookup"><span data-stu-id="9e754-137">**Snapshot data included for all volumes**: This behavior is seen only if you are running version earlier than Update 3.</span></span> <span data-ttu-id="9e754-138">針對所有磁碟區顯示的主要資料是每個磁碟區的主要資料與快照資料的總和。</span><span class="sxs-lookup"><span data-stu-id="9e754-138">The primary data shown for all the volumes is the sum of the primary data for each volume and the snapshot data.</span></span> <span data-ttu-id="9e754-139">針對指定的磁碟區顯示的主要資料只對應至在該磁碟區上配置的資料數量 (而不包含對應的磁碟區快照資料)。</span><span class="sxs-lookup"><span data-stu-id="9e754-139">The primary data shown for a given volume corresponds to only the amount of data allocated on the volume (and does not include the corresponding volume snapshot data).</span></span>
  
    <span data-ttu-id="9e754-140">這也可以由下列方程式來說明：</span><span class="sxs-lookup"><span data-stu-id="9e754-140">This can also be explained by the following equation:</span></span>
  
    <bpt id="p1">*</bpt>Primary data (All volumes) = Sum of (Primary data (volume i) + Size of snapshot data (volume i))<ept id="p1">*</ept>
  
    <bpt id="p1">*</bpt>where, Primary data (volume i) = Size of primary data allocated to volume i<ept id="p1">*</ept>
  
    <span data-ttu-id="9e754-143">如果透過服務刪除快照，將會在背景中以非同步方式進行刪除。</span><span class="sxs-lookup"><span data-stu-id="9e754-143">If the snapshots are deleted through the service, the deletion is done asynchronously in the background.</span></span> <span data-ttu-id="9e754-144">刪除快照之後，可能需要一些時間才會更新磁碟區資料大小。</span><span class="sxs-lookup"><span data-stu-id="9e754-144">It may take some time for the volume data size to be updated following the snapshot deletion.</span></span> 
  
    <span data-ttu-id="9e754-145">如果執行的是 Update 3 或更新版本，則磁碟區資料就不會包含快照資料。</span><span class="sxs-lookup"><span data-stu-id="9e754-145">If running Update 3 or later, then the snapshot data is not included in the volume data.</span></span> <span data-ttu-id="9e754-146">主要使用率的計算方式如下︰</span><span class="sxs-lookup"><span data-stu-id="9e754-146">And the primary utilization is calculated as follows:</span></span>
  
    <span data-ttu-id="9e754-147">*主要資料 (所有磁碟區) = (主要資料 (磁碟區 i)) 的總和</span><span class="sxs-lookup"><span data-stu-id="9e754-147">*Primary data (All volumes) = Sum of (Primary data (volume i)</span></span>
  
    <bpt id="p1">*</bpt>where, Primary data (volume i) = Size of primary data allocated to volume i<ept id="p1">*</ept>
* <span data-ttu-id="9e754-149">**所有磁碟區中包含已停用監視的磁碟區**：如果您的裝置上有已關閉監視的磁碟區，圖表中將不會有這些個別磁碟區的監視資料。</span><span class="sxs-lookup"><span data-stu-id="9e754-149">**Volumes with monitoring disabled included in all volumes**: If you have volumes on your device for which monitoring is turned off, the monitoring data for these individual volumes will not be available in the charts.</span></span> <span data-ttu-id="9e754-150">不過，圖表中所有磁碟區的資料會包含已關閉監視功能的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e754-150">However, the data for all volumes in the chart includes the volumes for which monitoring is turned off.</span></span> 
* <span data-ttu-id="9e754-151">**所有磁碟區的資料包含已刪除且具有即時關聯備份的磁碟區**：如果刪除包含快照資料的磁碟區，但關聯的快照仍然存在，您就可能看到不相符。</span><span class="sxs-lookup"><span data-stu-id="9e754-151">**Deleted volumes with live associated backups included for all volumes**: If volumes containing snapshot data are deleted but the associated snapshots still exist, then you may see a mismatch.</span></span>
* <span data-ttu-id="9e754-152">**所有磁碟區的資料包含已刪除的磁碟區**：在某些情況下，舊磁碟區即使在被刪除後仍然會存在。</span><span class="sxs-lookup"><span data-stu-id="9e754-152">**Deleted volumes included for all volumes**: In some instances, old volumes may exist even though these were deleted.</span></span> <span data-ttu-id="9e754-153">刪除的效果無法呈現，而裝置可能會顯示較低的可用容量。</span><span class="sxs-lookup"><span data-stu-id="9e754-153">The effect of deletion is not seen and the device may show lower available capacity.</span></span> <span data-ttu-id="9e754-154">您必須連絡「Microsoft 支援服務」以移除這些磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e754-154">You need to contact Microsoft Support to remove these volumes.</span></span>

<span data-ttu-id="9e754-155">下表顯示建立雲端快照集前後 StorSimple 裝置的主要儲存體容量使用率。</span><span class="sxs-lookup"><span data-stu-id="9e754-155">The following charts show the primary storage capacity utilization of a StorSimple device before and after a cloud snapshot was taken.</span></span> <span data-ttu-id="9e754-156">由於這只是磁碟區資料，因此雲端快照不應變更主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="9e754-156">As this is just volume data, a cloud snapshot should not change the primary storage.</span></span> <span data-ttu-id="9e754-157">如您所見，由於建立雲端快照集的緣故，圖表顯示的主要容量使用率沒有差別。</span><span class="sxs-lookup"><span data-stu-id="9e754-157">As you can see, the chart shows no difference in the primary capacity utilization as a result of taking a cloud snapshot.</span></span> <span data-ttu-id="9e754-158">雲端快照是在下午 2:00 左右開始在該裝置上建立。</span><span class="sxs-lookup"><span data-stu-id="9e754-158">The cloud snapshot started at around 2:00 pm on that device.</span></span>

![建立雲端快照集前的主要容量使用率](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![建立雲端快照集後的主要容量使用率](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

<span data-ttu-id="9e754-161">如果您執行的是 Update 2 或更新版本，就能夠依個別磁碟區、所有磁碟區、所有階層式磁碟區以及所有固定在本機的磁碟區，細分主要儲存體容量使用率，如以下所示。</span><span class="sxs-lookup"><span data-stu-id="9e754-161">If you are running Update 2 or higher, you can break down the primary storage capacity utilization by an individual volume, all volumes, all tiered volumes, and all locally pinned volumes as shown below.</span></span> <span data-ttu-id="9e754-162">如果依所有固定在本機的磁碟區來細分，您將能快速地確認已用完多少本機層。</span><span class="sxs-lookup"><span data-stu-id="9e754-162">Breaking down by all locally pinned volumes will allow you to quickly ascertain how much of the local tier is used up.</span></span>

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a><span data-ttu-id="9e754-164">雲端儲存體容量使用率</span><span class="sxs-lookup"><span data-stu-id="9e754-164">Cloud storage capacity utilization</span></span>
<span data-ttu-id="9e754-165">這些圖表顯示雲端儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="9e754-165">These charts show the amount of cloud storage used.</span></span> <span data-ttu-id="9e754-166">這項資料會進行重複資料刪除和壓縮。</span><span class="sxs-lookup"><span data-stu-id="9e754-166">This data is deduplicated and compressed.</span></span> <span data-ttu-id="9e754-167">此數量包含雲端快照集，其可能包含未反映在任何主要磁碟區且針對舊版或必要保留用途而保留的資料。</span><span class="sxs-lookup"><span data-stu-id="9e754-167">This amount includes cloud snapshots which might contain data that isn't reflected in any primary volume and is kept for legacy or required retention purposes.</span></span> <span data-ttu-id="9e754-168">您可以比較主要儲存體和雲端儲存體的耗用圖表來了解資料減少速率，雖然數字並不精確。</span><span class="sxs-lookup"><span data-stu-id="9e754-168">You can compare the primary and cloud storage consumption figures to get an idea of the data reduction rate, although the number will not be exact.</span></span> <span data-ttu-id="9e754-169">下表顯示建立雲端快照集前後 StorSimple 裝置的雲端儲存體容量使用率。</span><span class="sxs-lookup"><span data-stu-id="9e754-169">The following charts show the cloud storage capacity utilization of a StorSimple device before and after a cloud snapshot was taken.</span></span> <span data-ttu-id="9e754-170">雲端快照集在下午 2:00 左右於該裝置上開始建立，您可以看到雲端容量使用率在同時間飆升，從 5.73 MB 增加至 4.04 GB。</span><span class="sxs-lookup"><span data-stu-id="9e754-170">The cloud snapshot started at around 2:00 pm on that device and you can see the cloud capacity utilization shot up at the same time, increasing from 5.73 MB to 4.04 GB.</span></span>

![建立雲端快照集前的雲端容量使用率](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![建立雲端快照集後的雲端容量使用率](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a><span data-ttu-id="9e754-173">裝置儲存體容量使用率</span><span class="sxs-lookup"><span data-stu-id="9e754-173">Device storage capacity utilization</span></span>
<span data-ttu-id="9e754-174">這些圖表顯示裝置的總使用率，此使用率因為包含了 SSD 線性層，所以會高於主要儲存體使用率。</span><span class="sxs-lookup"><span data-stu-id="9e754-174">These charts show the total utilization for the device, which will be more than primary storage utilization because it includes the SSD linear tier.</span></span> <span data-ttu-id="9e754-175">這個階層包含也存在於裝置上其他階層中的資料量。</span><span class="sxs-lookup"><span data-stu-id="9e754-175">This tier contains an amount of data that also exists on the device's other tiers.</span></span> <span data-ttu-id="9e754-176">SSD 線性層中的容量是重複使用的，因此當新資料進入時，舊資料會移至 HDD 層 (此時會進行重複資料刪除並壓縮)，再移至雲端。</span><span class="sxs-lookup"><span data-stu-id="9e754-176">The capacity in the SSD linear tier is cycled so that when new data comes in, the old data is moved to the HDD tier (at which time it is deduplicated and compressed) and subsequently to the cloud.</span></span>

<span data-ttu-id="9e754-177">隨著時間過去，主要容量使用率和裝置容量使用率很可能會一起增加，直到資料開始分層到雲端。</span><span class="sxs-lookup"><span data-stu-id="9e754-177">Over time, primary capacity utilization and device capacity utilization will most likely increase together until the data begins to be tiered to the cloud.</span></span> <span data-ttu-id="9e754-178">此時，裝置容量使用率可能開始穩定停滯，但主要容量使用率將會因更多的資料寫入而增加。</span><span class="sxs-lookup"><span data-stu-id="9e754-178">At that point, the device capacity utilization will probably begin to plateau, but the primary capacity utilization will increase as more data is written.</span></span>

<span data-ttu-id="9e754-179">下表顯示建立雲端快照集前後 StorSimple 裝置的主要儲存體容量使用率。</span><span class="sxs-lookup"><span data-stu-id="9e754-179">The following charts show the primary storage capacity utilization of a StorSimple device before and after a cloud snapshot was taken.</span></span> <span data-ttu-id="9e754-180">雲端快照集在下午 2:00 開始建立，裝置容量使用率也在該時間開始減少。</span><span class="sxs-lookup"><span data-stu-id="9e754-180">The cloud snapshot started at 2:00 pm and the device capacity utilization started decreasing at that time.</span></span> <span data-ttu-id="9e754-181">裝置儲存體容量使用率從 11.58 GB 下降至 7.48 GB。</span><span class="sxs-lookup"><span data-stu-id="9e754-181">The device storage capacity utilization went down from 11.58 GB to 7.48 GB.</span></span> <span data-ttu-id="9e754-182">這表示很可能在線性 SSD 層中未壓縮的資料已刪除重複資料、壓縮，並移入 HDD 層。</span><span class="sxs-lookup"><span data-stu-id="9e754-182">This indicates that most likely the uncompressed data in the linear SSD tier was deduplicated, compressed, and moved into the HDD tier.</span></span> <span data-ttu-id="9e754-183">請注意，若裝置已在 SSD 和 HDD 層中有大量資料，您可能看不出減少的情況。</span><span class="sxs-lookup"><span data-stu-id="9e754-183">Note that if the device already has a large amount of data in both the SSD and HDD tiers, you may not see this decrease.</span></span> <span data-ttu-id="9e754-184">在此範例中，裝置僅有少量的資料。</span><span class="sxs-lookup"><span data-stu-id="9e754-184">In this example, the device has a small amount of data.</span></span>

![建立雲端快照集前的裝置容量使用率](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![建立雲端快照集後的裝置容量使用率](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a><span data-ttu-id="9e754-187">網路輸送量</span><span class="sxs-lookup"><span data-stu-id="9e754-187">Network throughput</span></span>
<span data-ttu-id="9e754-188">**網路輸送量** 會追蹤與從主機伺服器和裝置上的 iSCSI 啟動器網路介面傳輸之資料量有關，以及與在裝置和雲端之間傳輸之資料量有關的計量。</span><span class="sxs-lookup"><span data-stu-id="9e754-188">**Network throughput** tracks metrics related to the amount of data transferred from the iSCSI initiator network interfaces on the host server and the device and between the device and the cloud.</span></span> <span data-ttu-id="9e754-189">您可以針對裝置上的每一個 iSCSI 網路介面監視此計量。</span><span class="sxs-lookup"><span data-stu-id="9e754-189">You can monitor this metric for each of the iSCSI network interfaces on your device.</span></span>

<span data-ttu-id="9e754-190">下列圖表顯示您裝置上 Data 0 和 Data 4 (兩個都是 1 GbE 網路介面) 的網路輸送量。</span><span class="sxs-lookup"><span data-stu-id="9e754-190">The following charts show the network throughput for the Data 0 and Data 4, both 1 GbE network interfaces on your device.</span></span> <span data-ttu-id="9e754-191">在這種情況，Data 0 已啟用雲端功能，而資料 4 已啟用 iSCSI 功能。</span><span class="sxs-lookup"><span data-stu-id="9e754-191">In this instance, Data 0 was cloud-enabled whereas Data 4 was iSCSI-enabled.</span></span> <span data-ttu-id="9e754-192">您可以看到 StorSimple 裝置的輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="9e754-192">You can see both the inbound and the outbound traffic for your StorSimple device.</span></span> <span data-ttu-id="9e754-193">圖表中從下午 3:24 開始呈現水平線條，這是因為我們只每隔 5 分鐘收集一次資料，因此應忽略該線條。</span><span class="sxs-lookup"><span data-stu-id="9e754-193">The flat line in the chart starting from 3:24 pm is owing to the fact that we gather data only every 5 minutes and should be ignored.</span></span> 

![Data4 的網路輸送量](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Data4 的網路輸送量](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a><span data-ttu-id="9e754-196">裝置效能</span><span class="sxs-lookup"><span data-stu-id="9e754-196">Device performance</span></span>
<span data-ttu-id="9e754-197">**裝置效能** 會追蹤與您裝置的效能有關的計量。</span><span class="sxs-lookup"><span data-stu-id="9e754-197">**Device performance** tracks metrics related to the performance of your device.</span></span> <span data-ttu-id="9e754-198">下列圖表顯示生產環境中裝置的 CPU 使用率統計資料。</span><span class="sxs-lookup"><span data-stu-id="9e754-198">The following chart shows the CPU utilization stats for a device in production.</span></span>

![裝置的 CPU 使用率](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a><span data-ttu-id="9e754-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e754-200">Next steps</span></span>
* <span data-ttu-id="9e754-201">了解如何 [使用 StorSimple Manager 服務裝置儀表板](storsimple-device-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="9e754-201">Learn how to [use the StorSimple Manager service device dashboard](storsimple-device-dashboard.md).</span></span>
* <span data-ttu-id="9e754-202">了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="9e754-202">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

