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
# <a name="use-hello-storsimple-device-manager-service-toomonitor-your-storsimple-device"></a>使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 toomonitor
## <a name="overview"></a>概觀
在您於 StorSimple 解決方案內，您可以使用 hello StorSimple 裝置管理員服務 toomonitor 特定裝置。 您可以建立自訂根據 I/O 效能、 容量使用量、 網路輸送量和裝置效能度量的圖表，並將這些 toohello 儀表板釘選。 如需詳細資訊，請移至太[自訂入口網站儀表板](/articles/azure-portal/azure-portal-dashboards.md)。

tooview hello 監視資訊的特定裝置 hello Azure 入口網站中選取 hello StorSimple 裝置管理員服務。 從 hello 的裝置清單，選取您的裝置，然後跳過**監視器**。 您可以看見 hello**容量**，**使用量**，和**效能**hello 選裝置的圖表。

## <a name="capacity"></a>容量
**容量**曲目 hello 佈建的空間和 hello hello 裝置上剩餘的空間。 固定在本機或分層，這時會顯示 hello 剩餘容量。

佈建的 hello 和剩餘的容量會進一步細分分層和本機固定磁碟區。 每個磁碟區，hello 佈建的容量並顯示 hello 剩餘 hello 裝置上的容量。

![IO 容量](./media/storsimple-8000-monitor-device/device-capacity.png)



## <a name="usage"></a>使用量
**使用量**曲目度量相關的 toohello hello 磁碟區、 磁碟區容器或裝置使用的資料儲存空間量。 您可以建立 hello 容量使用率，您主要的儲存體、 雲端存放裝置，或您的裝置儲存體為基礎的報表。 容量使用率可以在特定磁碟區、特定磁碟區容器，或所有磁碟區容器上測量。
根據預設，會報告 hello 過去 24 小時內的使用方式。 您可以編輯 hello 圖表 toochange hello 持續時間的 hello 透過從選取的報告使用量：
* 過去 24 小時
* 過去 7 天
* 過去 30 天
* 過去 90 天
* 去年


主要 hello、 雲端和本機儲存體使用可以得到如下所述：

### <a name="primary-storage-usage"></a>主要儲存體使用量
這些圖表顯示 hello 之前進行重複資料刪除和壓縮 hello 資料寫入 tooStorSimple 磁碟區的資料量。 您可以檢視 hello 單一磁碟區或磁碟區容器中的所有磁碟區所使用的主要儲存體。 hello 主要儲存體，使用進一步細分主要分層式儲存體使用與主要固定在本機儲存體使用。

hello 下列圖表顯示 hello StorSimple 裝置之前和之後的雲端快照的拍攝用的主要儲存體。 因為這是只有磁碟區資料，雲端快照集不應該變更 hello 主要儲存體。 如您所見，hello 圖表可顯示 hello 主要分層式或固定在本機儲存體中使用的雲端快照的結果沒有差別。 在大約 50 的下午 11： 該裝置上，啟動 hello 雲端快照。

![建立雲端快照集後的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-after-cloudsnapshot.png)

如果您現在執行 IO hello 連接主機 tooyour StorSimple 裝置上，您會看到主要的分層式儲存體中增加或本機主要釘選視使用的儲存體 （分層或固定在本機） 的磁碟區時您 hello 將資料寫入。 以下是 StorSimple 裝置的 hello 主要儲存體使用量圖表。 這在裝置上，啟動服務的 hello StorSimple 主機在大約 2:30 pm 寫入 hello 裝置上為分層磁碟區上。 您可以看到 hello 尖峰 hello 寫入位元組/s 中對應 toohello IO hello 主機上執行。

![在階層式磁碟區執行 IO 時的效能](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

如果您看一下 hello 主要分層式儲存體使用，而 hello 主要固定在本機使用量保持不變，因為沒有已註冊的任何寫入提供 hello 裝置上不服務 toohello 固定在本機磁碟區。

![階層式磁碟區上執行 IO 時的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-io-from-initiator.png)

如果您正在更新 3 或更新版本中，您可以細分 hello 主要的儲存容量使用率的個別磁碟區、 所有磁碟區、 所有的階層式磁碟區和所有本機固定磁碟區如下所示。 所有在本機固定磁碟區可讓您細分 tooquickly 確定 hello 本機層中有多少用完。

![所有階層式磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/monitor-usage3.png)

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/monitor-usage4.png)

您可以進一步按一下每個 hello hello 清單中的磁碟區，並查看 hello 對應使用量。

![所有固定在本機之磁碟區的主要容量使用率](./media/storsimple-8000-monitor-device/device-primary-storage-usage-by-volume.png)

### <a name="cloud-storage-usage"></a>雲端儲存體使用量
這些圖表顯示 hello 用的雲端儲存空間量。 這項資料會進行重複資料刪除和壓縮。 此數量包含雲端快照集，其可能包含未反映在任何主要磁碟區且針對舊版或必要保留用途而保留的資料。 您可以比較 hello 主要和雲端儲存體耗用量圖表 tooget 了解 hello 減少資料的速率，雖然 hello 數目不會精確。

hello 下列圖表顯示 hello 雲端儲存空間利用率 StorSimple 裝置的雲端快照製作時。

* 開始於大約上午 11:50 該裝置上的 hello 雲端快照集，您可以看到之前 hello 雲端快照集，不沒有使用任何雲端存放裝置。 
* 一次完成 hello 雲端快照，hello 雲端儲存體使用率擷取畫面設定 0.89 GB。 
* Hello 雲端快照集已在進行時，還有對應的尖峰中從裝置 toocloud hello IO。

    ![建立雲端快照集之前的雲端儲存體使用率](./media/storsimple-8000-monitor-device/device-cloud-storage-before-cloudsnapshot.png)

    ![建立雲端快照集之後的雲端儲存體使用率](./media/storsimple-8000-monitor-device/device-cloud-storage-after-cloudsnapshot.png)

    ![從裝置 toocloud 雲端快照集期間的 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)


### <a name="local-storage-usage"></a>本機儲存體使用量
這些圖表顯示 hello 裝置，將會是主要的存放裝置使用量超過因為它包含 hello SSD 線性層 hello 總使用率。 這一層包含也存在於 hello 裝置的其他層的資料數量。 讓其新的資料時，hello 舊資料移動的 toohello HDD 層 （此時它是重複資料刪除和壓縮） 以及後續 toohello 雲端重新 hello SSD 線性層中的 hello 容量。

經過一段時間，直到 hello 資料開始 toobe 最可能一起增加使用的使用和本機儲存體的主要儲存體分層 toohello 雲端。 此時，hello 本機儲存體使用可能會開始 tooplateau，但 hello 主要儲存體使用會增加更多的資料會寫入。

hello 下列圖表顯示 hello 用於 StorSimple 裝置的雲端快照製作時的主要儲存體。 hello 雲端快照集開始於上午 11:50，在該時間減少 hello 本機儲存體已啟動。 從 1.445 GB too1.09 GB 擺 hello 本機儲存體使用。 這表示，最有可能 hello hello 線性的 SSD 層中的未壓縮的資料已進行重複資料刪除、 壓縮，並移入 hello HDD 層。 請注意是否 hello 裝置已經有大量的 hello SSD 和 HDD 層中的資料，您可能無法看見此減少。 在此範例中，hello 裝置有小量的資料。

![建立雲端快照集之後的本機儲存體使用率](./media/storsimple-8000-monitor-device/device-local-storage-after-cloudsnapshot.png)

## <a name="performance"></a>效能
**效能**曲目度量相關 toohello 編號的讀取和寫入作業之間任一 hello iSCSI 啟動器介面 hello 主機伺服器、 hello 裝置或裝置 hello 與 hello 雲端上。 這項效能可以針對特定磁碟區、特定磁碟區容器，或所有磁碟區容器來測量。 不同的網路介面在裝置上，效能也包括 CPU 使用率和 hello 的網路輸送量。

### <a name="io-performance-for-initiator-toodevice"></a>啟動器 toodevice I/O 效能
hello 下圖顯示之所有 hello 磁碟區的實際執行裝置 hello 啟動器 tooyour 裝置 hello I/O。 hello 繪製的度量資訊會讀取和寫入位元組 / 秒。 您也可以將讀取、寫入和未完成的 IO，或將讀取延遲和寫入延遲，繪製成圖表。

![啟動器 toodevice 的 IO 效能](./media/storsimple-8000-monitor-device/device-io-from-initiator.png)

### <a name="io-performance-for-device-toocloud"></a>裝置 toocloud I/O 效能
Hello 相同的裝置 hello I/O 作業所繪製的 hello hello 裝置 toohello 雲端資料的所有 hello 磁碟區容器。 在此裝置，hello 資料僅位於 hello 線性層，執行任何動作已溢出 toohello 雲端。 沒有裝置 toohello 雲端來源讀取寫入作業。 因此，hello 尖峰 hello 圖表會在對應的 hello 活動訊號檢查 hello 裝置與 hello 服務之間的 toohello 頻率 5 分鐘的間隔。

針對 hello 相同的裝置的雲端快照當時所進行的磁碟區資料起始上午 11:50。 這會導致從 hello 裝置 toohello 雲端中的資料流程。 寫入 toohello 雲端服務中這個持續時間。 hello IO 圖表可顯示尖峰 hello 寫入位元組/s 對應 toohello 當 hello 快照集執行時間。

![從裝置 toocloud 雲端快照集期間的 IO](./media/storsimple-8000-monitor-device/device-io-to-cloud-during-cloudsnapshot.png)

### <a name="network-throughput-for-device-network-interfaces"></a>裝置網路介面的網路輸送量
**網路輸送量**從 hello iSCSI 啟動器網路介面 hello 主機伺服器、 裝置 hello 和 hello 裝置與 hello 雲端之間傳送追蹤度量相關的 toohello 資料量。 您的裝置上，您可以針對每個 hello iSCSI 網路介面監視此標準。

下列圖表顯示 hello 網路輸送量 hello Data 0、 1 1 GbE 網路裝置，這是這兩個具備雲端功能 （預設值） 的 hello 和 iSCSI 功能。 此裝置上年 6 月 14 下午大約 9 中，已到 (在取得快照集時間的點 tootiering 正在沒有雲端到 hello 雲端 hello 機制 toomove hello 資料) 會產生 IO 提供 toohello 雲端 hello 雲端的階層式資料。 Hello 同一時間而大多數 hello 網路流量是輸出 toohello 雲端 hello 網路輸送量圖表中沒有對應的尖峰。

![Data 0 的網路輸送量](./media/storsimple-8000-monitor-device/device-network-throughput-data0.png)

如果看一下 hello Data 1 介面輸送量圖表，另一個 1 GbE 網路介面已啟用 iSCSI，則這個持續時間時發生幾乎沒有網路流量。

![Data 1 的網路輸送量](./media/storsimple-8000-monitor-device/device-network-throughput-data1.png)


## <a name="cpu-utilization-for-device"></a>裝置的 CPU 使用率
**CPU 使用率**曲目度量相關裝置上使用的 toohello CPU。 hello 下圖顯示 hello CPU 使用率統計資料的裝置在生產環境中。

![裝置的 CPU 使用率](./media/storsimple-8000-monitor-device/device-cpu-utilization.png)



## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello StorSimple 裝置管理員服務裝置儀表板](storsimple-device-dashboard.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

