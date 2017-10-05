---
title: "監視 StorSimple 8000 系列裝置 | Microsoft Docs"
description: "說明如何使用 StorSimple 裝置管理員服務來監視使用量、I/O 效能和容量使用率。"
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
ms.date: 08/02/2017
ms.author: alkohli
ms.openlocfilehash: ac11c6c8532007ee40db128dd9933c99a32a9420
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-device-manager-service-to-monitor-your-storsimple-device"></a><span data-ttu-id="beb8c-103">使用 StorSimple 裝置管理員服務監視 StorSimple 裝置</span><span class="sxs-lookup"><span data-stu-id="beb8c-103">Use the StorSimple Device Manager service to monitor your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="beb8c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="beb8c-104">Overview</span></span>
<span data-ttu-id="beb8c-105">您可以使用 StorSimple 裝置管理員服務來監視您 StorSimple 解決方案中的特定裝置。</span><span class="sxs-lookup"><span data-stu-id="beb8c-105">You can use the StorSimple Device Manager service to monitor specific devices within your StorSimple solution.</span></span> <span data-ttu-id="beb8c-106">您可以根據 I/O 效能、容量使用率、網路輸送量，以及裝置效能計量建立自訂圖表，並且將這些圖表釘選到儀表板。</span><span class="sxs-lookup"><span data-stu-id="beb8c-106">You can create custom charts based on I/O performance, capacity utilization, network throughput, and device performance metrics and pin those to the dashboard.</span></span> <span data-ttu-id="beb8c-107">如需詳細資訊，請移至[自訂入口網站儀表板](/articles/azure-portal/azure-portal-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="beb8c-107">For more information, go to [customize your portal dashboard](/articles/azure-portal/azure-portal-dashboards.md).</span></span>

<span data-ttu-id="beb8c-108">若要檢視特定裝置的監視資訊，請在 Azure 入口網站中，選取 [StorSimple 裝置管理員服務]。</span><span class="sxs-lookup"><span data-stu-id="beb8c-108">To view the monitoring information for a specific device, in the Azure portal, select the StorSimple Device Manager service.</span></span> <span data-ttu-id="beb8c-109">從裝置清單中選取您的裝置，然後移至 [監視]。</span><span class="sxs-lookup"><span data-stu-id="beb8c-109">From the list of devices, select your device and then go to **Monitor**.</span></span> <span data-ttu-id="beb8c-110">然後您會看見所選裝置的 [容量]、[使用量] 和 [效能] 圖表。</span><span class="sxs-lookup"><span data-stu-id="beb8c-110">You can then see the **Capacity**, **Usage**, and **Performance** charts for the selected device.</span></span>

## <a name="capacity"></a><span data-ttu-id="beb8c-111">容量</span><span class="sxs-lookup"><span data-stu-id="beb8c-111">Capacity</span></span>
<span data-ttu-id="beb8c-112">**容量**追蹤裝置上佈建的空間與剩餘的空間。</span><span class="sxs-lookup"><span data-stu-id="beb8c-112">**Capacity** tracks the provisioned space and the space remaining on the device.</span></span> <span data-ttu-id="beb8c-113">然後剩餘的容量會顯示為固定在本機或階層式。</span><span class="sxs-lookup"><span data-stu-id="beb8c-113">The remaining capacity is then displayed as locally pinned or tiered.</span></span>

<span data-ttu-id="beb8c-114">佈建的容量和剩餘的容量會進一步細分為階層式磁碟區和固定在本機的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="beb8c-114">The provisioned and remaining capacity is further broken down by tiered and locally pinned volumes.</span></span> <span data-ttu-id="beb8c-115">針對每個磁碟區，會顯示裝置上佈建的容量和剩餘的容量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-115">For each volume, the provisioned capacity and the remaining capacity on the device is displayed.</span></span>

![IO 容量](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a><span data-ttu-id="beb8c-117">使用量</span><span class="sxs-lookup"><span data-stu-id="beb8c-117">Usage</span></span>
<span data-ttu-id="beb8c-118">**使用量**追蹤由磁碟區、磁碟區容器，或裝置所使用之資料儲存體空間數量的相關計量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-118">**Usage** tracks metrics related to the amount of data storage space that is used by the volumes, volume containers, or device.</span></span> <span data-ttu-id="beb8c-119">您可以根據您的主要儲存體、雲端儲存體，或裝置儲存空間的容量使用率來建立報告。</span><span class="sxs-lookup"><span data-stu-id="beb8c-119">You can create reports based on the capacity utilization of your primary storage, your cloud storage, or your device storage.</span></span> <span data-ttu-id="beb8c-120">容量使用率可以在特定磁碟區、特定磁碟區容器，或所有磁碟區容器上測量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-120">Capacity utilization can be measured on a specific volume, a specific volume container, or all volume containers.</span></span>
<span data-ttu-id="beb8c-121">預設會報告過去 24 小時的使用量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-121">By default, the usage for past 24 hours is reported.</span></span> <span data-ttu-id="beb8c-122">您可以從下列項目選取來編輯圖表，以變更報告使用量的持續時間：</span><span class="sxs-lookup"><span data-stu-id="beb8c-122">You can edit the chart to change the duration over which the usage is reported by selecting from:</span></span>
* <span data-ttu-id="beb8c-123">過去 24 小時</span><span class="sxs-lookup"><span data-stu-id="beb8c-123">Past 24 hours</span></span>
* <span data-ttu-id="beb8c-124">過去 7 天</span><span class="sxs-lookup"><span data-stu-id="beb8c-124">Past 7 days</span></span>
* <span data-ttu-id="beb8c-125">過去 30 天</span><span class="sxs-lookup"><span data-stu-id="beb8c-125">Past 30 days</span></span>
* <span data-ttu-id="beb8c-126">過去 90 天</span><span class="sxs-lookup"><span data-stu-id="beb8c-126">Past 90 days</span></span>
* <span data-ttu-id="beb8c-127">去年</span><span class="sxs-lookup"><span data-stu-id="beb8c-127">Past year</span></span>


<span data-ttu-id="beb8c-128">使用的主要、雲端及本機儲存體的說明如下：</span><span class="sxs-lookup"><span data-stu-id="beb8c-128">The primary, cloud, and local storage used can be described as follows:</span></span>

### <a name="primary-storage-usage"></a><span data-ttu-id="beb8c-129">主要儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="beb8c-129">Primary storage usage</span></span>
<span data-ttu-id="beb8c-130">這些圖表顯示在進行重複資料刪除和壓縮之前寫入 StorSimple 磁碟區的資料量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-130">These charts show the amount of data written to StorSimple volumes before the data is deduplicated and compressed.</span></span> <span data-ttu-id="beb8c-131">您可以檢視磁碟區容器中所有磁碟區或單一磁碟區所使用的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="beb8c-131">You can view the primary storage used by all volumes in a volume container or for a single volume.</span></span> <span data-ttu-id="beb8c-132">使用的主要儲存體會進一步細分為使用的主要階層式存放區，以及使用的主要本機固定存放區。</span><span class="sxs-lookup"><span data-stu-id="beb8c-132">The primary storage used is further broken down by primary tiered storage used and primary locally pinned storage used.</span></span>

<span data-ttu-id="beb8c-133">下表顯示建立雲端快照集前後 StorSimple 裝置的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="beb8c-133">The following charts show the primary storage used for a StorSimple device before and after a cloud snapshot was taken.</span></span> <span data-ttu-id="beb8c-134">由於這只是磁碟區資料，因此雲端快照不應變更主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="beb8c-134">As this is just volume data, a cloud snapshot should not change the primary storage.</span></span> <span data-ttu-id="beb8c-135">如您所見，由於建立雲端快照集的緣故，圖表顯示使用的主要階層式存放區或使用的主要本機固定存放區並沒有差別。</span><span class="sxs-lookup"><span data-stu-id="beb8c-135">As you can see, the chart shows no difference in the primary tiered or locally pinned storage used as a result of taking a cloud snapshot.</span></span> <span data-ttu-id="beb8c-136">雲端快照是在下午 11:50 左右開始在該裝置上建立。</span><span class="sxs-lookup"><span data-stu-id="beb8c-136">The cloud snapshot started at around 11:50 pm on that device.</span></span>

![建立雲端快照集後的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

<span data-ttu-id="beb8c-138">如果您現在在連線到 StorSimple 裝置的主機上執行 IO，視您將資料寫入哪個磁碟區 (階層式或本機固定) 而定，將看到使用的主要階層式存放區或本機固定存放區會增加。</span><span class="sxs-lookup"><span data-stu-id="beb8c-138">If you now run IO on the host connected to your StorSimple device, you will see an increase in primary tiered storage or primary locally pinned storage used depending upon which volumes (tiered or locally pinned) you write the data to.</span></span> <span data-ttu-id="beb8c-139">以下是 StorSimple 裝置的主要儲存體使用量圖表。</span><span class="sxs-lookup"><span data-stu-id="beb8c-139">Here are the primary storage usage charts for a StorSimple device.</span></span> <span data-ttu-id="beb8c-140">在此裝置上，StorSimple 主機在下午大約 2:30，在裝置上的階層式磁碟區開始執行寫入。</span><span class="sxs-lookup"><span data-stu-id="beb8c-140">On this device, the StorSimple host started serving writes at around 2:30 pm on a tiered volume on the device.</span></span> <span data-ttu-id="beb8c-141">您可以看到寫入的每秒位元組出現峰值，對應至主機上執行的 IO。</span><span class="sxs-lookup"><span data-stu-id="beb8c-141">You can see the peak in the write bytes/s corresponding to the IO running on the host.</span></span>

![在階層式磁碟區執行 IO 時的效能](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

<span data-ttu-id="beb8c-143">如果您看使用的主要階層式存放區已經增加，但是主要本機固定的使用量還是維持不變，這是因為沒有執行寫入到裝置上的本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="beb8c-143">If you look at the primary tiered storage used, that has gone up whereas the primary locally pinned usage stays unchanged as there are no writes served to the locally pinned volumes on the device.</span></span>

![階層式磁碟區上執行 IO 時的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

<span data-ttu-id="beb8c-145">如果您執行的是 Update 3 或更新版本，就能夠依個別磁碟區、所有磁碟區、所有階層式磁碟區以及所有固定在本機的磁碟區，細分主要儲存體容量使用率，如以下所示。</span><span class="sxs-lookup"><span data-stu-id="beb8c-145">If you are running Update 3 or higher, you can break down the primary storage capacity utilization by an individual volume, all volumes, all tiered volumes, and all locally pinned volumes as shown below.</span></span> <span data-ttu-id="beb8c-146">如果依所有固定在本機的磁碟區來細分，您將能快速地確認已用完多少本機層。</span><span class="sxs-lookup"><span data-stu-id="beb8c-146">Breaking down by all locally pinned volumes will allow you to quickly ascertain how much of the local tier is used up.</span></span>

![所有階層式磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/monitor-usage4.png)

<span data-ttu-id="beb8c-149">您可以進一步按一下清單中的每個磁碟區，查看對應的使用量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-149">You can further click on each of the volumes in the list and see the corresponding usage.</span></span>

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a><span data-ttu-id="beb8c-151">雲端儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="beb8c-151">Cloud storage usage</span></span>
<span data-ttu-id="beb8c-152">這些圖表顯示雲端儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-152">These charts show the amount of cloud storage used.</span></span> <span data-ttu-id="beb8c-153">這項資料會進行重複資料刪除和壓縮。</span><span class="sxs-lookup"><span data-stu-id="beb8c-153">This data is deduplicated and compressed.</span></span> <span data-ttu-id="beb8c-154">此數量包含雲端快照集，其可能包含未反映在任何主要磁碟區且針對舊版或必要保留用途而保留的資料。</span><span class="sxs-lookup"><span data-stu-id="beb8c-154">This amount includes cloud snapshots which might contain data that isn't reflected in any primary volume and is kept for legacy or required retention purposes.</span></span> <span data-ttu-id="beb8c-155">您可以比較主要儲存體和雲端儲存體的耗用圖表來了解資料減少速率，雖然數字並不精確。</span><span class="sxs-lookup"><span data-stu-id="beb8c-155">You can compare the primary and cloud storage consumption figures to get an idea of the data reduction rate, although the number will not be exact.</span></span>

<span data-ttu-id="beb8c-156">下表顯示建立雲端快照集時，StorSimple 裝置的雲端儲存體使用率。</span><span class="sxs-lookup"><span data-stu-id="beb8c-156">The following charts show the cloud storage utilization of a StorSimple device when a cloud snapshot was taken.</span></span>

* <span data-ttu-id="beb8c-157">雲端快照集在上午大約 11:50 在該裝置上啟動，您可以看到在雲端快照集之前，還沒有使用的雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="beb8c-157">The cloud snapshot started at around 11:50 am on that device and you can see that before the cloud snapshot, there was no cloud storage used.</span></span> 
* <span data-ttu-id="beb8c-158">雲端快照集完成之後，雲端儲存體使用率瞬間上升到 0.89 GB。</span><span class="sxs-lookup"><span data-stu-id="beb8c-158">Once the cloud snapshot completed, the cloud storage utilization shot up 0.89 GB.</span></span> 
* <span data-ttu-id="beb8c-159">雲端快照集進行時，從裝置到雲端的 IO 也有一個對應的峰值。</span><span class="sxs-lookup"><span data-stu-id="beb8c-159">While the cloud snapshot was in progress, there is also a corresponding peak in the IO from device to cloud.</span></span>

    ![建立雲端快照集之前的雲端儲存體使用率](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![建立雲端快照集之後的雲端儲存體使用率](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![建立雲端快照集期間，從裝置到雲端的 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a><span data-ttu-id="beb8c-163">本機儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="beb8c-163">Local storage usage</span></span>
<span data-ttu-id="beb8c-164">這些圖表顯示裝置的總使用率，此使用率因為包含了 SSD 線性層，所以會高於主要儲存體使用量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-164">These charts show the total utilization for the device, which will be more than primary storage usage because it includes the SSD linear tier.</span></span> <span data-ttu-id="beb8c-165">這個階層包含也存在於裝置上其他階層中的資料量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-165">This tier contains an amount of data that also exists on the device's other tiers.</span></span> <span data-ttu-id="beb8c-166">SSD 線性層中的容量是重複使用的，因此當新資料進入時，舊資料會移至 HDD 層 (此時會進行重複資料刪除並壓縮)，再移至雲端。</span><span class="sxs-lookup"><span data-stu-id="beb8c-166">The capacity in the SSD linear tier is cycled so that when new data comes in, the old data is moved to the HDD tier (at which time it is deduplicated and compressed) and subsequently to the cloud.</span></span>

<span data-ttu-id="beb8c-167">隨著時間過去，使用的主要儲存體和使用的本機儲存體很可能會一起增加，直到資料開始分層到雲端。</span><span class="sxs-lookup"><span data-stu-id="beb8c-167">Over time, primary storage used and local storage used will most likely increase together until the data begins to be tiered to the cloud.</span></span> <span data-ttu-id="beb8c-168">此時，使用的本機儲存體可能開始穩定停滯，但使用的主要儲存體將會因更多的資料寫入而增加。</span><span class="sxs-lookup"><span data-stu-id="beb8c-168">At that point, the local storage used will probably begin to plateau, but the primary storage used will increase as more data is written.</span></span>

<span data-ttu-id="beb8c-169">下表顯示建立雲端快照集時，StorSimple 裝置使用的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="beb8c-169">The following charts show the primary storage used for a StorSimple device when a cloud snapshot was taken.</span></span> <span data-ttu-id="beb8c-170">雲端快照集在上午 11:50 開始建立，本機儲存體也在該時間開始減少。</span><span class="sxs-lookup"><span data-stu-id="beb8c-170">The cloud snapshot started at 11:50 am and the local storage started decreasing at that time.</span></span> <span data-ttu-id="beb8c-171">使用的本機儲存體從 1.445 GB 下降到 1.09 GB。</span><span class="sxs-lookup"><span data-stu-id="beb8c-171">The local storage used went down from 1.445 GB to 1.09 GB.</span></span> <span data-ttu-id="beb8c-172">這表示很可能在線性 SSD 層中未壓縮的資料已刪除重複資料、壓縮，並移入 HDD 層。</span><span class="sxs-lookup"><span data-stu-id="beb8c-172">This indicates that most likely the uncompressed data in the linear SSD tier was deduplicated, compressed, and moved into the HDD tier.</span></span> <span data-ttu-id="beb8c-173">請注意，若裝置已在 SSD 和 HDD 層中有大量資料，您可能看不出減少的情況。</span><span class="sxs-lookup"><span data-stu-id="beb8c-173">Note that if the device already has a large amount of data in both the SSD and HDD tiers, you may not see this decrease.</span></span> <span data-ttu-id="beb8c-174">在此範例中，裝置僅有少量的資料。</span><span class="sxs-lookup"><span data-stu-id="beb8c-174">In this example, the device has a small amount of data.</span></span>

![建立雲端快照集之後的本機儲存體使用率](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a><span data-ttu-id="beb8c-176">效能</span><span class="sxs-lookup"><span data-stu-id="beb8c-176">Performance</span></span>
<span data-ttu-id="beb8c-177">**效能**追蹤主機伺服器上 iSCSI 啟動器介面與裝置之間或裝置與雲端之間，與讀取和寫入作業數目相關的計量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-177">**Performance** tracks metrics related to the number of read and write operations between either the iSCSI initiator interfaces on the host server and the device or the device and the cloud.</span></span> <span data-ttu-id="beb8c-178">這項效能可以針對特定磁碟區、特定磁碟區容器，或所有磁碟區容器來測量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-178">This performance can be measured for a specific volume, a specific volume container, or all volume containers.</span></span> <span data-ttu-id="beb8c-179">效能也包括裝置上的 CPU 使用率和不同網路介面的網路輸送量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-179">Performance also includes CPU utilization and Network throughput for the various network interfaces on your device.</span></span>

### <a name="io-performance-for-initiator-to-device"></a><span data-ttu-id="beb8c-180">啟動器到裝置的 I/O 效能</span><span class="sxs-lookup"><span data-stu-id="beb8c-180">I/O performance for initiator to device</span></span>
<span data-ttu-id="beb8c-181">下表顯示生產環境裝置之所有磁碟區中的裝置啟動器 I/O。</span><span class="sxs-lookup"><span data-stu-id="beb8c-181">The chart below shows the I/O for the initiator to your device for all the volumes for a production device.</span></span> <span data-ttu-id="beb8c-182">繪製的計量是每秒讀取和寫入的位元組。</span><span class="sxs-lookup"><span data-stu-id="beb8c-182">The metrics plotted are read and write bytes per second.</span></span> <span data-ttu-id="beb8c-183">您也可以將讀取、寫入和未完成的 IO，或將讀取延遲和寫入延遲，繪製成圖表。</span><span class="sxs-lookup"><span data-stu-id="beb8c-183">You can also chart read, write, and outstanding IO, or read and write latencies.</span></span>

![啟動器到裝置的 IO 效能](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-to-cloud"></a><span data-ttu-id="beb8c-185">裝置到雲端的 I/O 效能</span><span class="sxs-lookup"><span data-stu-id="beb8c-185">I/O performance for device to cloud</span></span>
<span data-ttu-id="beb8c-186">就相同裝置而言，所繪製的 I/O 作業是針對所有磁碟區容器從裝置到雲端的資料。</span><span class="sxs-lookup"><span data-stu-id="beb8c-186">For the same device, the I/O operations are plotted for the data from the device to the cloud for all the volume containers.</span></span> <span data-ttu-id="beb8c-187">在此裝置上，資料僅位於線性層內且並未溢出至雲端。</span><span class="sxs-lookup"><span data-stu-id="beb8c-187">On this device, the data is only in the linear tier and nothing has spilled to the cloud.</span></span> <span data-ttu-id="beb8c-188">從裝置到雲端並未發生讀寫作業。</span><span class="sxs-lookup"><span data-stu-id="beb8c-188">There are no read-write operations occurring from device to the cloud.</span></span> <span data-ttu-id="beb8c-189">因此，圖表中尖峰的間隔是 5 分鐘，這和裝置與服務之間的活動訊號檢查頻率對應。</span><span class="sxs-lookup"><span data-stu-id="beb8c-189">Therefore, the peaks in the chart are at an interval of 5 minutes that corresponds to the frequency at which the heartbeat is checked between the device and the service.</span></span>

<span data-ttu-id="beb8c-190">針對相同的裝置，磁碟區資料的雲端快照集從上午 11:50 開始建立。</span><span class="sxs-lookup"><span data-stu-id="beb8c-190">For the same device, a cloud snapshot was taken for volume data starting at 11:50 am.</span></span> <span data-ttu-id="beb8c-191">這會導致資料從裝置流向雲端。</span><span class="sxs-lookup"><span data-stu-id="beb8c-191">This resulted in data flowing from the device to the cloud.</span></span> <span data-ttu-id="beb8c-192">在這段期間會提供雲端寫入服務。</span><span class="sxs-lookup"><span data-stu-id="beb8c-192">Writes were served to the cloud in this duration.</span></span> <span data-ttu-id="beb8c-193">IO 圖表顯示建立快照集時，在每秒寫入位元組出現峰值所對應的時間。</span><span class="sxs-lookup"><span data-stu-id="beb8c-193">The IO chart shows a peak in the Write Bytes/s corresponding to the time when the snapshot was taken.</span></span>

![建立雲端快照集期間，從裝置到雲端的 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a><span data-ttu-id="beb8c-195">裝置網路介面的網路輸送量</span><span class="sxs-lookup"><span data-stu-id="beb8c-195">Network throughput for device network interfaces</span></span>
<span data-ttu-id="beb8c-196">**網路輸送量** 會追蹤與從主機伺服器和裝置上的 iSCSI 啟動器網路介面傳輸之資料量有關，以及與在裝置和雲端之間傳輸之資料量有關的計量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-196">**Network throughput** tracks metrics related to the amount of data transferred from the iSCSI initiator network interfaces on the host server and the device and between the device and the cloud.</span></span> <span data-ttu-id="beb8c-197">您可以針對裝置上的每一個 iSCSI 網路介面監視此計量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-197">You can monitor this metric for each of the iSCSI network interfaces on your device.</span></span>

<span data-ttu-id="beb8c-198">下列圖表顯示裝置上 Data 0、1 1 GbE 網路的網路輸送量，此網路同時具備雲端功能 (預設) 和 iSCSI 功能。</span><span class="sxs-lookup"><span data-stu-id="beb8c-198">The following charts show the network throughput for the Data 0, 1 1 GbE network on your device, which was both cloud-enabled (default) and iSCSI-enabled.</span></span> <span data-ttu-id="beb8c-199">此裝置在 6 月 14 日下午大約 9 點，資料分層到雲端 (當時沒有建立任何雲端快照集，表示分層是將資料移動到雲端的機制)，產生傳送到雲端的 IO。</span><span class="sxs-lookup"><span data-stu-id="beb8c-199">On this device on June 14 at around 9 pm, data was tiered into the cloud (no cloud snapshots were taken at that time which points to tiering being the mechanism to move the data into the cloud) which resulted in IO being served to the cloud.</span></span> <span data-ttu-id="beb8c-200">網路輸送量圖表在同一時間有對應的峰值，且大部分的網路流量是輸出到雲端。</span><span class="sxs-lookup"><span data-stu-id="beb8c-200">There is a corresponding peak in the network throughput graph for the same time and most of the network traffic is outbound to the cloud.</span></span>

![Data 0 的網路輸送量](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

<span data-ttu-id="beb8c-202">如果我們看 Data 1 介面的輸送量圖表 (另一個只啟用 iSCSI 的 1 GbE 網路介面)，在這段期間幾乎沒有網路流量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-202">If we look at the Data 1 interface throughput chart, another 1 GbE network interface which was only iSCSI-enabled, then there was virtually no network traffic in this duration.</span></span>

![Data 1 的網路輸送量](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a><span data-ttu-id="beb8c-204">裝置的 CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="beb8c-204">CPU utilization for device</span></span>
<span data-ttu-id="beb8c-205">**CPU 使用率**追蹤裝置上與使用的 CPU 相關的計量。</span><span class="sxs-lookup"><span data-stu-id="beb8c-205">**CPU utilization** tracks metrics related to the CPU utilized on your device.</span></span> <span data-ttu-id="beb8c-206">下列圖表顯示生產環境中裝置的 CPU 使用率統計資料。</span><span class="sxs-lookup"><span data-stu-id="beb8c-206">The following chart shows the CPU utilization stats for a device in production.</span></span>

![裝置的 CPU 使用率](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a><span data-ttu-id="beb8c-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="beb8c-208">Next steps</span></span>
* <span data-ttu-id="beb8c-209">了解如何[使用 StorSimple 裝置管理員服務裝置儀表板](storsimple-device-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="beb8c-209">Learn how to [use the StorSimple Device Manager service device dashboard](storsimple-device-dashboard.md).</span></span>
* <span data-ttu-id="beb8c-210">了解如何[使用 StorSimple 裝置管理員服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="beb8c-210">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

