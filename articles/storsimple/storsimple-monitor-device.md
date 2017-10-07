---
title: "aaaMonitor StorSimple 裝置 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Manager 服務 toomonitor I/O 效能、 容量使用量、 網路輸送量和裝置的效能。"
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
ms.openlocfilehash: c1f614a7f52728650bfadb3335435b8b5a17e6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-your-storsimple-device"></a>使用您的 StorSimple 裝置 hello StorSimple Manager 服務 toomonitor
## <a name="overview"></a>概觀
您可以在您於 StorSimple 解決方案內使用 hello StorSimple Manager 服務 toomonitor 特定裝置。 您可以根據 I/O 效能、容量使用率、網路輸送量，以及裝置效能計量建立自訂圖表。 

tooview hello 監視特定的裝置，請在 hello Azure 傳統入口網站，選取 hello StorSimple Manager 服務中的資訊。 按一下 hello**監視器**索引標籤，然後再從 hello 的裝置清單中選取。 hello**監視器**頁面包含下列資訊的 hello。

## <a name="io-performance"></a>I/O 效能
**I/O 效能**曲目度量相關 toohello 編號的讀取和寫入作業之間任一 hello iSCSI 啟動器介面 hello 主機伺服器、 hello 裝置或裝置 hello 與 hello 雲端上。 這項效能可以針對特定磁碟區、特定磁碟區容器，或所有磁碟區容器來測量。

hello 下圖顯示之所有 hello 磁碟區的實際執行裝置 hello 啟動器 tooyour 裝置 hello I/O。 hello 繪製的度量資訊會讀取和寫入位元組 / 秒、 讀取和寫入 IO 作業每秒，並讀取和寫入延遲。

![從起始端 toodevice IO 效能](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_InitiatorTODevice_For_AllVolumesM.png)

Hello 相同的裝置 hello I/O 作業所繪製的 hello hello 裝置 toohello 雲端資料的所有 hello 磁碟區容器。 在此裝置，hello 資料僅位於 hello 線性層，執行任何動作已溢出 toohello 雲端。 沒有裝置 toohello 雲端來源讀取寫入作業。 因此，hello 尖峰 hello 圖表會在對應的 hello 活動訊號檢查 hello 裝置與 hello 服務之間的 toohello 頻率 5 分鐘的間隔。 

![從裝置 toocloud IO 效能](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainersM.png)

針對 hello 相同的裝置的雲端快照當時所進行的磁碟區資料在下午 2:00 開始。 這會導致從 hello 裝置 toohello 雲端中的資料流程。 讀取寫入 toohello 雲端服務中這個持續時間。 hello IO 圖表可顯示尖峰 hello 中對應的各種標準 toohello 拍攝 hello 快照時的時間。 

![裝置 toocloud 雲端快照集之後的 IO 效能](./media/storsimple-monitor-device/StorSimple_IO_Performance_For_DeviceTOCloud_For_AllVolumeContainers2M.png)

## <a name="capacity-utilization"></a>容量使用率
**容量使用率**曲目度量相關的 toohello hello 磁碟區、 磁碟區容器或裝置使用的資料儲存空間量。 您可以建立 hello 容量使用率，您主要的儲存體、 雲端存放裝置，或您的裝置儲存體為基礎的報表。 容量使用率可以在特定磁碟區、特定磁碟區容器，或所有磁碟區容器上測量。

主要的 hello、 雲端和裝置儲存容量可以得到如下所述：

### <a name="primary-storage-capacity-utilization"></a>主要儲存體容量使用率
這些圖表顯示 hello 之前進行重複資料刪除和壓縮 hello 資料寫入 tooStorSimple 磁碟區的資料量。 您可以檢視 hello 主要儲存體使用率，所有磁碟區或單一磁碟區。

當您在這些情況下檢視 hello 主要儲存體磁碟區容量使用率圖表的所有磁碟區與每個 hello 個別磁碟區和 hello 主要資料的總和時，hello 兩個數字之間可能有不相符。 hello 總主要的資料在所有磁碟區上可能不會加總 hello 主要資料的個別磁碟區 hello toohello 總和。 這可能是因為 tooone hello 以下的：

* **所有磁碟區的資料包含快照資料**︰只有當您執行的版本是比 Update 3 舊的版本時，才會發生此行為。 hello 主要資料所示為 hello 的所有磁碟區是每個磁碟區的 hello 主要資料與 hello 快照集資料 hello 總和。 指定磁碟區所顯示的 hello 主要資料對應 tooonly hello hello 磁碟區上配置的資料量 （而且不包含 hello 對應的磁碟區快照集資料）。
  
    這也可以說明的下列方程式 hello:
  
    <bpt id="p1">*</bpt>Primary data (All volumes) = Sum of (Primary data (volume i) + Size of snapshot data (volume i))<ept id="p1">*</ept>
  
    *where、 主要資料 （磁碟區 i） = toovolume 配置的主要資料的大小我*
  
    如果透過 hello 服務將會刪除 hello 快照集，是以非同步方式在 hello 背景完成 hello 刪除。 可能需要一些時間的 hello 磁碟區的資料大小 toobe hello 快照刪除下列更新。 
  
    如果 3 或更新版本，請執行更新，然後 hello 快照集的資料不納入 hello 磁碟區資料。 和 hello 主要使用率的計算方式如下：
  
    *主要資料 (所有磁碟區) = (主要資料 (磁碟區 i)) 的總和
  
    *where、 主要資料 （磁碟區 i） = toovolume 配置的主要資料的大小我*
* **使用監視停用中包含磁碟區的所有磁碟區**： 如果您有磁碟區的監視已關閉裝置上，監視這些個別的磁碟區資料的 hello 將無法使用 hello 圖表中。 不過，在 hello 圖表中的所有磁碟區的 hello 資料包含 hello 磁碟區的監視已關閉。 
* **刪除磁碟區與即時相關聯的備份包含所有磁碟區**： 如果包含快照集資料的磁碟區被刪除，但是相關聯的 hello 快照集仍然存在，則您可能會看到不相符。
* **所有磁碟區的資料包含已刪除的磁碟區**：在某些情況下，舊磁碟區即使在被刪除後仍然會存在。 已刪除的 hello 效果不會出現並 hello 裝置可能會顯示較低的可用容量。 您需要 toocontact Microsoft 支援服務 tooremove 這些磁碟區。

hello 下列圖表顯示 hello 的主要儲存體容量使用率的 StorSimple 裝置之前和之後拍攝的雲端快照。 因為這是只有磁碟區資料，雲端快照集不應該變更 hello 主要儲存體。 如您所見，hello 圖表可顯示 hello 主要容量使用率的雲端快照的結果之間並無差異。 在大約 2:00 pm 該裝置上，啟動 hello 雲端快照集。

![建立雲端快照集前的主要容量使用率](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes2M.png)

![建立雲端快照集後的主要容量使用率](./media/storsimple-monitor-device/StorSimple_PrimaryCapacityUtil_For_AllVolumes1M.png)

如果您正在更新 2 或更高版本，您可以將分解 hello 主要的儲存容量使用率的個別磁碟區、 所有磁碟區、 所有的階層式磁碟區和所有本機固定磁碟區如下所示。 所有在本機固定磁碟區可讓您細分 tooquickly 確定 hello 本機層中有多少用完。

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-monitor-device/localvolumes.png)

### <a name="cloud-storage-capacity-utilization"></a>雲端儲存體容量使用率
這些圖表顯示 hello 用的雲端儲存空間量。 這項資料會進行重複資料刪除和壓縮。 此數量包含雲端快照集，其可能包含未反映在任何主要磁碟區且針對舊版或必要保留用途而保留的資料。 您可以比較 hello 主要和雲端儲存體耗用量圖表 tooget 了解 hello 減少資料的速率，雖然 hello 數目不會精確。 hello 下列圖表顯示 hello 雲端儲存容量使用率的 StorSimple 裝置之前和之後拍攝的雲端快照。 hello 雲端快照集開始於大約 2:00 pm 該裝置上，您可以看到 hello 雲端容量使用率擷取畫面在 hello 相同 5.73 MB too4.04 GB 遞增的時間。

![建立雲端快照集前的雲端容量使用率](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers2M.png)

![建立雲端快照集後的雲端容量使用率](./media/storsimple-monitor-device/StorSimple_CloudCapacityUtil_For_AllVolumeContainers1M.png)

### <a name="device-storage-capacity-utilization"></a>裝置儲存體容量使用率
這些圖表顯示 hello 裝置，將多個主要儲存體使用率因為它包含 hello SSD 線性層 hello 總使用率。 這一層包含也存在於 hello 裝置的其他層的資料數量。 讓其新的資料時，hello 舊資料移動的 toohello HDD 層 （此時它是重複資料刪除和壓縮） 以及後續 toohello 雲端重新 hello SSD 線性層中的 hello 容量。

經過一段時間，主要的容量使用率和裝置容量使用率很可能會增加一起直到 hello 資料開始 toobe 分層 toohello 雲端。 此時，hello 裝置容量使用率可能會開始 tooplateau，但寫入更多資料時，會增加 hello 主要容量使用率。

hello 下列圖表顯示 hello 的主要儲存體容量使用率的 StorSimple 裝置之前和之後拍攝的雲端快照。 在下午 2:00 啟動 hello 雲端快照集和 hello 裝置容量使用率開始在該時間減少。 hello 裝置儲存容量使用率停擺從 11.58 GB too7.48 GB。 這表示，最有可能 hello hello 線性的 SSD 層中的未壓縮的資料已進行重複資料刪除、 壓縮，並移入 hello HDD 層。 請注意是否 hello 裝置已經有大量的 hello SSD 和 HDD 層中的資料，您可能無法看見此減少。 在此範例中，hello 裝置有小量的資料。

![建立雲端快照集前的裝置容量使用率](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil2M.png)

![建立雲端快照集後的裝置容量使用率](./media/storsimple-monitor-device/StorSimple_DeviceCapacityUtil1M.png)

## <a name="network-throughput"></a>網路輸送量
**網路輸送量**從 hello iSCSI 啟動器網路介面 hello 主機伺服器、 裝置 hello 和 hello 裝置與 hello 雲端之間傳送追蹤度量相關的 toohello 資料量。 您的裝置上，您可以針對每個 hello iSCSI 網路介面監視此標準。

下列圖表顯示 hello hello Data 0 和 Data 4，在您的裝置上的這兩個 1 GbE 網路介面的網路輸送量的 hello。 在這種情況，Data 0 已啟用雲端功能，而資料 4 已啟用 iSCSI 功能。 您可以看到這兩個輸入與 hello StorSimple 裝置的輸出流量的 hello。 從下午 3:24 開始的 hello 圖表中的 hello 平穩直線與 toohello 事實我們僅每 5 分鐘收集資料，應予忽略。 

![Data4 的網路輸送量](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data0M.png)

![Data4 的網路輸送量](./media/storsimple-monitor-device/StorSimple_NetworkThroughput_Data4M.png)

## <a name="device-performance"></a>裝置效能
**裝置效能**曲目度量相關 toohello 效能，您的裝置。 hello 下圖顯示 hello CPU 使用率統計資料的裝置在生產環境中。

![裝置的 CPU 使用率](./media/storsimple-monitor-device/StorSimple_DeviceMonitor_DevicePerformance1M.png)

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello StorSimple Manager 服務裝置儀表板](storsimple-device-dashboard.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

