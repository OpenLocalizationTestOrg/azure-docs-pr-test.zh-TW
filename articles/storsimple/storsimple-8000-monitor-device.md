---
title: "aaaMonitor StorSimple 8000 系列裝置 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple 裝置管理員服務 toomonitor 使用量、 I/O 效能和容量使用率。"
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
ms.openlocfilehash: 092dab8dd301c50fc12316b4031a8d1b34fab876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a><span data-ttu-id="89d6c-103">使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 toomonitor</span><span class="sxs-lookup"><span data-stu-id="89d6c-103">Use hello StorSimple Device Manager service toomonitor your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="89d6c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="89d6c-104">Overview</span></span>
<span data-ttu-id="89d6c-105">在您於 StorSimple 解決方案內，您可以使用 hello StorSimple 裝置管理員服務 toomonitor 特定裝置。</span><span class="sxs-lookup"><span data-stu-id="89d6c-105">You can use hello StorSimple Device Manager service toomonitor specific devices within your StorSimple solution.</span></span> <span data-ttu-id="89d6c-106">您可以建立自訂根據 I/O 效能、 容量使用量、 網路輸送量和裝置效能度量的圖表，並將這些 toohello 儀表板釘選。</span><span class="sxs-lookup"><span data-stu-id="89d6c-106">You can create custom charts based on I/O performance, capacity utilization, network throughput, and device performance metrics and pin those toohello dashboard.</span></span> <span data-ttu-id="89d6c-107">如需詳細資訊，請移至太[自訂入口網站儀表板](/articles/azure-portal/azure-portal-dashboards.md)。</span><span class="sxs-lookup"><span data-stu-id="89d6c-107">For more information, go too[customize your portal dashboard](/articles/azure-portal/azure-portal-dashboards.md).</span></span>

<span data-ttu-id="89d6c-108">tooview hello 監視資訊的特定裝置 hello Azure 入口網站中選取 hello StorSimple 裝置管理員服務。</span><span class="sxs-lookup"><span data-stu-id="89d6c-108">tooview hello monitoring information for a specific device, in hello Azure portal, select hello StorSimple Device Manager service.</span></span> <span data-ttu-id="89d6c-109">從 hello 的裝置清單，選取您的裝置，然後跳過**監視器**。</span><span class="sxs-lookup"><span data-stu-id="89d6c-109">From hello list of devices, select your device and then go too**Monitor**.</span></span> <span data-ttu-id="89d6c-110">您可以看見 hello**容量**，**使用量**，和**效能**hello 選裝置的圖表。</span><span class="sxs-lookup"><span data-stu-id="89d6c-110">You can then see hello **Capacity**, **Usage**, and **Performance** charts for hello selected device.</span></span>

## <a name="capacity"></a><span data-ttu-id="89d6c-111">容量</span><span class="sxs-lookup"><span data-stu-id="89d6c-111">Capacity</span></span>
<span data-ttu-id="89d6c-112">**容量**曲目 hello 佈建的空間和 hello hello 裝置上剩餘的空間。</span><span class="sxs-lookup"><span data-stu-id="89d6c-112">**Capacity** tracks hello provisioned space and hello space remaining on hello device.</span></span> <span data-ttu-id="89d6c-113">固定在本機或分層，這時會顯示 hello 剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-113">hello remaining capacity is then displayed as locally pinned or tiered.</span></span>

<span data-ttu-id="89d6c-114">佈建的 hello 和剩餘的容量會進一步細分分層和本機固定磁碟區。</span><span class="sxs-lookup"><span data-stu-id="89d6c-114">hello provisioned and remaining capacity is further broken down by tiered and locally pinned volumes.</span></span> <span data-ttu-id="89d6c-115">每個磁碟區，hello 佈建的容量並顯示 hello 剩餘 hello 裝置上的容量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-115">For each volume, hello provisioned capacity and hello remaining capacity on hello device is displayed.</span></span>

![IO 容量](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a><span data-ttu-id="89d6c-117">使用量</span><span class="sxs-lookup"><span data-stu-id="89d6c-117">Usage</span></span>
<span data-ttu-id="89d6c-118">**使用量**曲目度量相關的 toohello hello 磁碟區、 磁碟區容器或裝置使用的資料儲存空間量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-118">**Usage** tracks metrics related toohello amount of data storage space that is used by hello volumes, volume containers, or device.</span></span> <span data-ttu-id="89d6c-119">您可以建立 hello 容量使用率，您主要的儲存體、 雲端存放裝置，或您的裝置儲存體為基礎的報表。</span><span class="sxs-lookup"><span data-stu-id="89d6c-119">You can create reports based on hello capacity utilization of your primary storage, your cloud storage, or your device storage.</span></span> <span data-ttu-id="89d6c-120">容量使用率可以在特定磁碟區、特定磁碟區容器，或所有磁碟區容器上測量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-120">Capacity utilization can be measured on a specific volume, a specific volume container, or all volume containers.</span></span>
<span data-ttu-id="89d6c-121">根據預設，會報告 hello 過去 24 小時內的使用方式。</span><span class="sxs-lookup"><span data-stu-id="89d6c-121">By default, hello usage for past 24 hours is reported.</span></span> <span data-ttu-id="89d6c-122">您可以編輯 hello 圖表 toochange hello 持續時間的 hello 透過從選取的報告使用量：</span><span class="sxs-lookup"><span data-stu-id="89d6c-122">You can edit hello chart toochange hello duration over which hello usage is reported by selecting from:</span></span>
* <span data-ttu-id="89d6c-123">過去 24 小時</span><span class="sxs-lookup"><span data-stu-id="89d6c-123">Past 24 hours</span></span>
* <span data-ttu-id="89d6c-124">過去 7 天</span><span class="sxs-lookup"><span data-stu-id="89d6c-124">Past 7 days</span></span>
* <span data-ttu-id="89d6c-125">過去 30 天</span><span class="sxs-lookup"><span data-stu-id="89d6c-125">Past 30 days</span></span>
* <span data-ttu-id="89d6c-126">過去 90 天</span><span class="sxs-lookup"><span data-stu-id="89d6c-126">Past 90 days</span></span>
* <span data-ttu-id="89d6c-127">去年</span><span class="sxs-lookup"><span data-stu-id="89d6c-127">Past year</span></span>


<span data-ttu-id="89d6c-128">主要 hello、 雲端和本機儲存體使用可以得到如下所述：</span><span class="sxs-lookup"><span data-stu-id="89d6c-128">hello primary, cloud, and local storage used can be described as follows:</span></span>

### <a name="primary-storage-usage"></a><span data-ttu-id="89d6c-129">主要儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="89d6c-129">Primary storage usage</span></span>
<span data-ttu-id="89d6c-130">這些圖表顯示 hello 之前進行重複資料刪除和壓縮 hello 資料寫入 tooStorSimple 磁碟區的資料量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-130">These charts show hello amount of data written tooStorSimple volumes before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="89d6c-131">您可以檢視 hello 單一磁碟區或磁碟區容器中的所有磁碟區所使用的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="89d6c-131">You can view hello primary storage used by all volumes in a volume container or for a single volume.</span></span> <span data-ttu-id="89d6c-132">hello 主要儲存體，使用進一步細分主要分層式儲存體使用與主要固定在本機儲存體使用。</span><span class="sxs-lookup"><span data-stu-id="89d6c-132">hello primary storage used is further broken down by primary tiered storage used and primary locally pinned storage used.</span></span>

<span data-ttu-id="89d6c-133">hello 下列圖表顯示 hello StorSimple 裝置之前和之後的雲端快照的拍攝用的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="89d6c-133">hello following charts show hello primary storage used for a StorSimple device before and after a cloud snapshot was taken.</span></span> <span data-ttu-id="89d6c-134">因為這是只有磁碟區資料，雲端快照集不應該變更 hello 主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="89d6c-134">As this is just volume data, a cloud snapshot should not change hello primary storage.</span></span> <span data-ttu-id="89d6c-135">如您所見，hello 圖表可顯示 hello 主要分層式或固定在本機儲存體中使用的雲端快照的結果沒有差別。</span><span class="sxs-lookup"><span data-stu-id="89d6c-135">As you can see, hello chart shows no difference in hello primary tiered or locally pinned storage used as a result of taking a cloud snapshot.</span></span> <span data-ttu-id="89d6c-136">在大約 50 的下午 11： 該裝置上，啟動 hello 雲端快照。</span><span class="sxs-lookup"><span data-stu-id="89d6c-136">hello cloud snapshot started at around 11:50 pm on that device.</span></span>

![建立雲端快照集後的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

<span data-ttu-id="89d6c-138">如果您現在執行 IO hello 連接主機 tooyour StorSimple 裝置上，您會看到主要的分層式儲存體中增加或本機主要釘選視使用的儲存體 （分層或固定在本機） 的磁碟區時您 hello 將資料寫入。</span><span class="sxs-lookup"><span data-stu-id="89d6c-138">If you now run IO on hello host connected tooyour StorSimple device, you will see an increase in primary tiered storage or primary locally pinned storage used depending upon which volumes (tiered or locally pinned) you write hello data to.</span></span> <span data-ttu-id="89d6c-139">以下是 StorSimple 裝置的 hello 主要儲存體使用量圖表。</span><span class="sxs-lookup"><span data-stu-id="89d6c-139">Here are hello primary storage usage charts for a StorSimple device.</span></span> <span data-ttu-id="89d6c-140">這在裝置上，啟動服務的 hello StorSimple 主機在大約 2:30 pm 寫入 hello 裝置上為分層磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="89d6c-140">On this device, hello StorSimple host started serving writes at around 2:30 pm on a tiered volume on hello device.</span></span> <span data-ttu-id="89d6c-141">您可以看到 hello 尖峰 hello 寫入位元組/s 中對應 toohello IO hello 主機上執行。</span><span class="sxs-lookup"><span data-stu-id="89d6c-141">You can see hello peak in hello write bytes/s corresponding toohello IO running on hello host.</span></span>

![在階層式磁碟區執行 IO 時的效能](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

<span data-ttu-id="89d6c-143">如果您看一下 hello 主要分層式儲存體使用，而 hello 主要固定在本機使用量保持不變，因為沒有已註冊的任何寫入提供 hello 裝置上不服務 toohello 固定在本機磁碟區。</span><span class="sxs-lookup"><span data-stu-id="89d6c-143">If you look at hello primary tiered storage used, that has gone up whereas hello primary locally pinned usage stays unchanged as there are no writes served toohello locally pinned volumes on hello device.</span></span>

![階層式磁碟區上執行 IO 時的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

<span data-ttu-id="89d6c-145">如果您正在更新 3 或更新版本中，您可以細分 hello 主要的儲存容量使用率的個別磁碟區、 所有磁碟區、 所有的階層式磁碟區和所有本機固定磁碟區如下所示。</span><span class="sxs-lookup"><span data-stu-id="89d6c-145">If you are running Update 3 or higher, you can break down hello primary storage capacity utilization by an individual volume, all volumes, all tiered volumes, and all locally pinned volumes as shown below.</span></span> <span data-ttu-id="89d6c-146">所有在本機固定磁碟區可讓您細分 tooquickly 確定 hello 本機層中有多少用完。</span><span class="sxs-lookup"><span data-stu-id="89d6c-146">Breaking down by all locally pinned volumes will allow you tooquickly ascertain how much of hello local tier is used up.</span></span>

![所有階層式磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/monitor-usage4.png)

<span data-ttu-id="89d6c-149">您可以進一步按一下每個 hello hello 清單中的磁碟區，並查看 hello 對應使用量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-149">You can further click on each of hello volumes in hello list and see hello corresponding usage.</span></span>

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a><span data-ttu-id="89d6c-151">雲端儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="89d6c-151">Cloud storage usage</span></span>
<span data-ttu-id="89d6c-152">這些圖表顯示 hello 用的雲端儲存空間量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-152">These charts show hello amount of cloud storage used.</span></span> <span data-ttu-id="89d6c-153">這項資料會進行重複資料刪除和壓縮。</span><span class="sxs-lookup"><span data-stu-id="89d6c-153">This data is deduplicated and compressed.</span></span> <span data-ttu-id="89d6c-154">此數量包含雲端快照集，其可能包含未反映在任何主要磁碟區且針對舊版或必要保留用途而保留的資料。</span><span class="sxs-lookup"><span data-stu-id="89d6c-154">This amount includes cloud snapshots which might contain data that isn't reflected in any primary volume and is kept for legacy or required retention purposes.</span></span> <span data-ttu-id="89d6c-155">您可以比較 hello 主要和雲端儲存體耗用量圖表 tooget 了解 hello 減少資料的速率，雖然 hello 數目不會精確。</span><span class="sxs-lookup"><span data-stu-id="89d6c-155">You can compare hello primary and cloud storage consumption figures tooget an idea of hello data reduction rate, although hello number will not be exact.</span></span>

<span data-ttu-id="89d6c-156">hello 下列圖表顯示 hello 雲端儲存空間利用率 StorSimple 裝置的雲端快照製作時。</span><span class="sxs-lookup"><span data-stu-id="89d6c-156">hello following charts show hello cloud storage utilization of a StorSimple device when a cloud snapshot was taken.</span></span>

* <span data-ttu-id="89d6c-157">開始於大約上午 11:50 該裝置上的 hello 雲端快照集，您可以看到之前 hello 雲端快照集，不沒有使用任何雲端存放裝置。</span><span class="sxs-lookup"><span data-stu-id="89d6c-157">hello cloud snapshot started at around 11:50 am on that device and you can see that before hello cloud snapshot, there was no cloud storage used.</span></span> 
* <span data-ttu-id="89d6c-158">一次完成 hello 雲端快照，hello 雲端儲存體使用率擷取畫面設定 0.89 GB。</span><span class="sxs-lookup"><span data-stu-id="89d6c-158">Once hello cloud snapshot completed, hello cloud storage utilization shot up 0.89 GB.</span></span> 
* <span data-ttu-id="89d6c-159">Hello 雲端快照集已在進行時，還有對應的尖峰中從裝置 toocloud hello IO。</span><span class="sxs-lookup"><span data-stu-id="89d6c-159">While hello cloud snapshot was in progress, there is also a corresponding peak in hello IO from device toocloud.</span></span>

    ![建立雲端快照集之前的雲端儲存體使用率](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![建立雲端快照集之後的雲端儲存體使用率](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![從裝置 toocloud 雲端快照集期間的 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a><span data-ttu-id="89d6c-163">本機儲存體使用量</span><span class="sxs-lookup"><span data-stu-id="89d6c-163">Local storage usage</span></span>
<span data-ttu-id="89d6c-164">這些圖表顯示 hello 裝置，將會是主要的存放裝置使用量超過因為它包含 hello SSD 線性層 hello 總使用率。</span><span class="sxs-lookup"><span data-stu-id="89d6c-164">These charts show hello total utilization for hello device, which will be more than primary storage usage because it includes hello SSD linear tier.</span></span> <span data-ttu-id="89d6c-165">這一層包含也存在於 hello 裝置的其他層的資料數量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-165">This tier contains an amount of data that also exists on hello device's other tiers.</span></span> <span data-ttu-id="89d6c-166">讓其新的資料時，hello 舊資料移動的 toohello HDD 層 （此時它是重複資料刪除和壓縮） 以及後續 toohello 雲端重新 hello SSD 線性層中的 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-166">hello capacity in hello SSD linear tier is cycled so that when new data comes in, hello old data is moved toohello HDD tier (at which time it is deduplicated and compressed) and subsequently toohello cloud.</span></span>

<span data-ttu-id="89d6c-167">經過一段時間，直到 hello 資料開始 toobe 最可能一起增加使用的使用和本機儲存體的主要儲存體分層 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="89d6c-167">Over time, primary storage used and local storage used will most likely increase together until hello data begins toobe tiered toohello cloud.</span></span> <span data-ttu-id="89d6c-168">此時，hello 本機儲存體使用可能會開始 tooplateau，但 hello 主要儲存體使用會增加更多的資料會寫入。</span><span class="sxs-lookup"><span data-stu-id="89d6c-168">At that point, hello local storage used will probably begin tooplateau, but hello primary storage used will increase as more data is written.</span></span>

<span data-ttu-id="89d6c-169">hello 下列圖表顯示 hello 用於 StorSimple 裝置的雲端快照製作時的主要儲存體。</span><span class="sxs-lookup"><span data-stu-id="89d6c-169">hello following charts show hello primary storage used for a StorSimple device when a cloud snapshot was taken.</span></span> <span data-ttu-id="89d6c-170">hello 雲端快照集開始於上午 11:50，在該時間減少 hello 本機儲存體已啟動。</span><span class="sxs-lookup"><span data-stu-id="89d6c-170">hello cloud snapshot started at 11:50 am and hello local storage started decreasing at that time.</span></span> <span data-ttu-id="89d6c-171">從 1.445 GB too1.09 GB 擺 hello 本機儲存體使用。</span><span class="sxs-lookup"><span data-stu-id="89d6c-171">hello local storage used went down from 1.445 GB too1.09 GB.</span></span> <span data-ttu-id="89d6c-172">這表示，最有可能 hello hello 線性的 SSD 層中的未壓縮的資料已進行重複資料刪除、 壓縮，並移入 hello HDD 層。</span><span class="sxs-lookup"><span data-stu-id="89d6c-172">This indicates that most likely hello uncompressed data in hello linear SSD tier was deduplicated, compressed, and moved into hello HDD tier.</span></span> <span data-ttu-id="89d6c-173">請注意是否 hello 裝置已經有大量的 hello SSD 和 HDD 層中的資料，您可能無法看見此減少。</span><span class="sxs-lookup"><span data-stu-id="89d6c-173">Note that if hello device already has a large amount of data in both hello SSD and HDD tiers, you may not see this decrease.</span></span> <span data-ttu-id="89d6c-174">在此範例中，hello 裝置有小量的資料。</span><span class="sxs-lookup"><span data-stu-id="89d6c-174">In this example, hello device has a small amount of data.</span></span>

![建立雲端快照集之後的本機儲存體使用率](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a><span data-ttu-id="89d6c-176">效能</span><span class="sxs-lookup"><span data-stu-id="89d6c-176">Performance</span></span>
<span data-ttu-id="89d6c-177">**效能**曲目度量相關 toohello 編號的讀取和寫入作業之間任一 hello iSCSI 啟動器介面 hello 主機伺服器、 hello 裝置或裝置 hello 與 hello 雲端上。</span><span class="sxs-lookup"><span data-stu-id="89d6c-177">**Performance** tracks metrics related toohello number of read and write operations between either hello iSCSI initiator interfaces on hello host server and hello device or hello device and hello cloud.</span></span> <span data-ttu-id="89d6c-178">這項效能可以針對特定磁碟區、特定磁碟區容器，或所有磁碟區容器來測量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-178">This performance can be measured for a specific volume, a specific volume container, or all volume containers.</span></span> <span data-ttu-id="89d6c-179">不同的網路介面在裝置上，效能也包括 CPU 使用率和 hello 的網路輸送量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-179">Performance also includes CPU utilization and Network throughput for hello various network interfaces on your device.</span></span>

### <a name="io-performance-for-initiator-toodevice"></a><span data-ttu-id="89d6c-180">啟動器 toodevice I/O 效能</span><span class="sxs-lookup"><span data-stu-id="89d6c-180">I/O performance for initiator toodevice</span></span>
<span data-ttu-id="89d6c-181">hello 下圖顯示之所有 hello 磁碟區的實際執行裝置 hello 啟動器 tooyour 裝置 hello I/O。</span><span class="sxs-lookup"><span data-stu-id="89d6c-181">hello chart below shows hello I/O for hello initiator tooyour device for all hello volumes for a production device.</span></span> <span data-ttu-id="89d6c-182">hello 繪製的度量資訊會讀取和寫入位元組 / 秒。</span><span class="sxs-lookup"><span data-stu-id="89d6c-182">hello metrics plotted are read and write bytes per second.</span></span> <span data-ttu-id="89d6c-183">您也可以將讀取、寫入和未完成的 IO，或將讀取延遲和寫入延遲，繪製成圖表。</span><span class="sxs-lookup"><span data-stu-id="89d6c-183">You can also chart read, write, and outstanding IO, or read and write latencies.</span></span>

![啟動器 toodevice 的 IO 效能](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a><span data-ttu-id="89d6c-185">裝置 toocloud I/O 效能</span><span class="sxs-lookup"><span data-stu-id="89d6c-185">I/O performance for device toocloud</span></span>
<span data-ttu-id="89d6c-186">Hello 相同的裝置 hello I/O 作業所繪製的 hello hello 裝置 toohello 雲端資料的所有 hello 磁碟區容器。</span><span class="sxs-lookup"><span data-stu-id="89d6c-186">For hello same device, hello I/O operations are plotted for hello data from hello device toohello cloud for all hello volume containers.</span></span> <span data-ttu-id="89d6c-187">在此裝置，hello 資料僅位於 hello 線性層，執行任何動作已溢出 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="89d6c-187">On this device, hello data is only in hello linear tier and nothing has spilled toohello cloud.</span></span> <span data-ttu-id="89d6c-188">沒有裝置 toohello 雲端來源讀取寫入作業。</span><span class="sxs-lookup"><span data-stu-id="89d6c-188">There are no read-write operations occurring from device toohello cloud.</span></span> <span data-ttu-id="89d6c-189">因此，hello 尖峰 hello 圖表會在對應的 hello 活動訊號檢查 hello 裝置與 hello 服務之間的 toohello 頻率 5 分鐘的間隔。</span><span class="sxs-lookup"><span data-stu-id="89d6c-189">Therefore, hello peaks in hello chart are at an interval of 5 minutes that corresponds toohello frequency at which hello heartbeat is checked between hello device and hello service.</span></span>

<span data-ttu-id="89d6c-190">針對 hello 相同的裝置的雲端快照當時所進行的磁碟區資料起始上午 11:50。</span><span class="sxs-lookup"><span data-stu-id="89d6c-190">For hello same device, a cloud snapshot was taken for volume data starting at 11:50 am.</span></span> <span data-ttu-id="89d6c-191">這會導致從 hello 裝置 toohello 雲端中的資料流程。</span><span class="sxs-lookup"><span data-stu-id="89d6c-191">This resulted in data flowing from hello device toohello cloud.</span></span> <span data-ttu-id="89d6c-192">寫入 toohello 雲端服務中這個持續時間。</span><span class="sxs-lookup"><span data-stu-id="89d6c-192">Writes were served toohello cloud in this duration.</span></span> <span data-ttu-id="89d6c-193">hello IO 圖表可顯示尖峰 hello 寫入位元組/s 對應 toohello 當 hello 快照集執行時間。</span><span class="sxs-lookup"><span data-stu-id="89d6c-193">hello IO chart shows a peak in hello Write Bytes/s corresponding toohello time when hello snapshot was taken.</span></span>

![從裝置 toocloud 雲端快照集期間的 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a><span data-ttu-id="89d6c-195">裝置網路介面的網路輸送量</span><span class="sxs-lookup"><span data-stu-id="89d6c-195">Network throughput for device network interfaces</span></span>
<span data-ttu-id="89d6c-196">**網路輸送量**從 hello iSCSI 啟動器網路介面 hello 主機伺服器、 裝置 hello 和 hello 裝置與 hello 雲端之間傳送追蹤度量相關的 toohello 資料量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-196">**Network throughput** tracks metrics related toohello amount of data transferred from hello iSCSI initiator network interfaces on hello host server and hello device and between hello device and hello cloud.</span></span> <span data-ttu-id="89d6c-197">您的裝置上，您可以針對每個 hello iSCSI 網路介面監視此標準。</span><span class="sxs-lookup"><span data-stu-id="89d6c-197">You can monitor this metric for each of hello iSCSI network interfaces on your device.</span></span>

<span data-ttu-id="89d6c-198">下列圖表顯示 hello 網路輸送量 hello Data 0、 1 1 GbE 網路裝置，這是這兩個具備雲端功能 （預設值） 的 hello 和 iSCSI 功能。</span><span class="sxs-lookup"><span data-stu-id="89d6c-198">hello following charts show hello network throughput for hello Data 0, 1 1 GbE network on your device, which was both cloud-enabled (default) and iSCSI-enabled.</span></span> <span data-ttu-id="89d6c-199">此裝置上年 6 月 14 下午大約 9 中，已到 (在取得快照集時間的點 tootiering 正在沒有雲端到 hello 雲端 hello 機制 toomove hello 資料) 會產生 IO 提供 toohello 雲端 hello 雲端的階層式資料。</span><span class="sxs-lookup"><span data-stu-id="89d6c-199">On this device on June 14 at around 9 pm, data was tiered into hello cloud (no cloud snapshots were taken at that time which points tootiering being hello mechanism toomove hello data into hello cloud) which resulted in IO being served toohello cloud.</span></span> <span data-ttu-id="89d6c-200">Hello 同一時間而大多數 hello 網路流量是輸出 toohello 雲端 hello 網路輸送量圖表中沒有對應的尖峰。</span><span class="sxs-lookup"><span data-stu-id="89d6c-200">There is a corresponding peak in hello network throughput graph for hello same time and most of hello network traffic is outbound toohello cloud.</span></span>

![Data 0 的網路輸送量](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

<span data-ttu-id="89d6c-202">如果看一下 hello Data 1 介面輸送量圖表，另一個 1 GbE 網路介面已啟用 iSCSI，則這個持續時間時發生幾乎沒有網路流量。</span><span class="sxs-lookup"><span data-stu-id="89d6c-202">If we look at hello Data 1 interface throughput chart, another 1 GbE network interface which was only iSCSI-enabled, then there was virtually no network traffic in this duration.</span></span>

![Data 1 的網路輸送量](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a><span data-ttu-id="89d6c-204">裝置的 CPU 使用率</span><span class="sxs-lookup"><span data-stu-id="89d6c-204">CPU utilization for device</span></span>
<span data-ttu-id="89d6c-205">**CPU 使用率**曲目度量相關裝置上使用的 toohello CPU。</span><span class="sxs-lookup"><span data-stu-id="89d6c-205">**CPU utilization** tracks metrics related toohello CPU utilized on your device.</span></span> <span data-ttu-id="89d6c-206">hello 下圖顯示 hello CPU 使用率統計資料的裝置在生產環境中。</span><span class="sxs-lookup"><span data-stu-id="89d6c-206">hello following chart shows hello CPU utilization stats for a device in production.</span></span>

![裝置的 CPU 使用率](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a><span data-ttu-id="89d6c-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89d6c-208">Next steps</span></span>
* <span data-ttu-id="89d6c-209">了解如何太[使用 hello StorSimple 裝置管理員服務裝置儀表板](storsimple-device-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="89d6c-209">Learn how too[use hello StorSimple Device Manager service device dashboard](storsimple-device-dashboard.md).</span></span>
* <span data-ttu-id="89d6c-210">了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。</span><span class="sxs-lookup"><span data-stu-id="89d6c-210">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

