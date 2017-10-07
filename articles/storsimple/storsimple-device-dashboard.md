---
title: "aaaUse hello StorSimple Manager 裝置儀表板 |Microsoft 文件"
description: "描述 hello StorSimple Manager 服務裝置儀表板和如何 toouse 它 tooview 儲存體度量和連接的起始端和尋找 hello 序號和 IQN。"
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
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>使用 StorSimple Manager 服務中的 hello 裝置儀表板  

## <a name="overview"></a>概觀
hello StorSimple Manager 裝置儀表板提供您特定的 StorSimple 裝置的資訊概觀，相較之下 toohello 服務儀表板，可讓您所有包含在 Microsoft Azure StorSimple 解決方案中的 hello 裝置的相關資訊。

![裝置儀表板頁面](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

hello 儀表板包含下列資訊的 hello:

* **圖表區域**– 您可以看到在 hello hello 儀表板頂端的 hello 圖表區域中的 hello 相關的儲存體度量。 在此圖中，您可以檢視度量 hello 總主要儲存體 （hello 由主機 tooyour 裝置寫入的資料量） 並 hello 總雲端經過一段時間的裝置所使用的存放裝置。
  
     在此內容中*主要儲存體*參照 toohello 總量 hello 主機寫入的資料，並可依磁碟區類型細分：*主要的階層式儲存體*同時包含在本機儲存資料和資料階層式的 toohello 雲端;*主要固定在本機儲存體*包含只在本機儲存的資料。 *雲端儲存體*，在 hello 相反，是 hello 的 hello 雲端中儲存的資料量總計的度量單位。 這包括分層式資料和備份。 請注意 hello 雲端中儲存的資料是重複資料刪除和壓縮，而主要儲存體指出 hello hello 資料重複資料刪除，且壓縮之前使用的儲存體的數量。 （您可以比較這些兩個數字 tooget hello 壓縮率的了解）。這兩個主要部署和雲端儲存體，hello 所示金額將會根據 hello 追蹤您所設定的頻率。 例如，如果您選擇一週頻率，然後 hello 圖表會顯示資料中每一天 hello 前一週。
  
     您可以設定 hello 圖表，如下所示：
  
  * 一段時間，請選取 hello 耗用的雲端儲存體 toosee hello 數量**CLOUD STORAGE USED**選項。 toosee hello 總儲存體已寫入 hello 主機上，選取 hello **PRIMARY 分層 STORAGE USED**和**主要在本機固定的儲存體使用**選項。 在 hello 圖中，選取這兩個選項。因此，hello 圖表可顯示雲端和主要儲存體數量。 請注意任何主要儲存體，使用先前 tooinstalling Update 2 由 hello **PRIMARY 分層 STORAGE USED**列。
  * 使用 hello 下拉式選單中的 hello 圖表 toospecify hello 右上角 1 週、 1 個月、 3 個月或 1 年的時間期間。 請注意，hello 最上層的圖表會隨即重新整理一次只能每日，並因此會反映 hello 前一天的總和。
    
    如需詳細資訊，請參閱[使用 hello StorSimple Manager 服務 toomonitor StorSimple 裝置](storsimple-monitor-device.md)。
* **使用量概觀**– 在 hello**使用量概觀**區域中，您可以看到 hello 的主要儲存體使用量，佈建的儲存體和為您的裝置 hello 最大儲存容量的 hello 數量。 藉由比較這些使用量數字 toohello 最大數量是可用的儲存體，您可以一目了然如果您需要 tooobtain 額外的存放裝置。 請注意，此概觀每隔 15 分鐘更新一次，因為更新頻率 hello 差異，可能會顯示不同的數字以外顯示 hello 圖表區域中，每日更新。 如需詳細資訊，請參閱[使用 hello StorSimple Manager 服務 toomonitor StorSimple 裝置](storsimple-monitor-device.md)。
* **警示**– hello**警示**區域包含裝置 hello 警示的概觀。 警示會依嚴重性分組，並提供一個計數，hello 數字，每個嚴重性層級的警示。 按一下 hello 警示嚴重性即會開啟 hello 已設定領域的檢視警示 索引標籤 tooshow 您只有 hello 這個裝置的該嚴重性層級的警示。
* **作業**– hello**作業**區域會顯示 hello 最近工作活動的結果。 這可讓您 hello 系統如預期地運作，或它可以讓您知道您需要 tootake 矯正措施。 按一下 toosee 最近完成之作業的詳細資訊**工作 hello 在過去 24 小時內成功**。
* hello**快速概覽**上 hello hello 儀表板的權限的區域會提供實用資訊，例如裝置機型、 序號、 狀態、 描述及磁碟區數目。

您也可以設定容錯移轉，並檢視連接的起始端從 hello 裝置儀表板。

hello 可以在此頁面執行的一般工作包括：

* 檢視連接的啟動器
* 尋找裝置序號 hello
* 尋找 hello 裝置目標 IQN

## <a name="view-connected-initiators"></a>檢視連接的啟動器
您可以檢視依序按一下 hello 以連接的 tooyour 裝置 hello iSCSI 啟動器**檢視連接的啟動器**hello 中提供連結**快速概覽**裝置儀表板的區域。 此頁面提供已成功連接 tooyour 裝置 hello 啟動器的表格清單。 對於每個啟動器，您可以查看：

* hello iSCSI 合格名稱 (IQN) 的 hello 連線起始端。
* hello hello 存取控制記錄 (ACR)，可讓這個連接之啟動器的名稱。
* hello hello IP 位址連線起始端。
* hello 網路介面的 hello 啟動器是連接的 tooon 存放裝置。 這些範圍可以從 DATA 0 tooDATA 5。
* 所有 hello 連接之啟動器的 hello 磁碟區允許 tooaccess 根據 toohello 目前的 ACR 組態。

如果您看到這份清單中未預期的啟動器或看不到 hello 預期是時，檢閱您的 ACR 組態。 最多 512 個起始端可以連接 tooyour 裝置。

## <a name="find-hello-device-serial-number"></a>尋找裝置序號 hello
當您在 hello 裝置上設定 Microsoft 多重路徑 I/O (MPIO) 時，您可能需要 hello 裝置序號。 執行下列步驟 toofind hello 裝置序號的 hello。

#### <a name="toofind-hello-device-serial-number"></a>toofind hello 裝置序號
1. 瀏覽過**裝置** > **儀表板**。
2. Hello 右窗格中的 hello 儀表板，找出 hello**快速概覽**區域。
3. 向下捲動並找出 hello 數列數字。

## <a name="find-hello-device-target-iqn"></a>尋找 hello 裝置目標 IQN
當您設定 StorSimple 裝置上的 hello Challenge Handshake 驗證通訊協定 (CHAP) 時，您可能需要 hello 裝置目標 IQN。 執行下列步驟 toofind hello 裝置目標 IQN hello。

### <a name="toofind-hello-device-target-iqn"></a>toofind hello 裝置目標 IQN
1. 瀏覽過**裝置** > **儀表板**。
2. Hello 右窗格中的 hello 儀表板，找出 hello**快速概覽**區域。
3. 向下捲動並找出 hello 目標 IQN。

## <a name="next-steps"></a>後續步驟
* 深入了解 hello [StorSimple Manager 服務儀表板](storsimple-service-dashboard.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

