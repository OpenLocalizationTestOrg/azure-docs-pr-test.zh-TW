---
title: "aaaUse StorSimple 8000 系列裝置摘要 |Microsoft 文件"
description: "描述 hello StorSimple 裝置管理員服務裝置摘要以及 toouse 它 tooview 儲存體度量和連接的起始端和尋找 hello 序號和 IQN。"
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>使用摘要 StorSimple 裝置管理員服務中的 hello 裝置

## <a name="overview"></a>概觀
hello StorSimple 裝置摘要刀鋒視窗可讓您針對特定的 StorSimple 裝置的資訊概觀，相較之下 toohello 服務摘要刀鋒視窗中，它將提供所有包含在 Microsoft Azure StorSimple 解決方案中的 hello 裝置的相關資訊。

hello 裝置摘要刀鋒視窗會提供摘要檢視的 StorSimple 8000 系列裝置註冊與給定 StorSimple 裝置管理員 中，反白顯示需要系統管理員的注意這些裝置問題。 本教學課程介紹 hello 裝置摘要刀鋒視窗，說明 hello 內容和函式，並說明您可以從這個刀鋒視窗中執行的 hello 工作。

hello 裝置摘要刀鋒視窗會顯示下列資訊的 hello:

![[裝置摘要] 刀鋒視窗](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>管理命令列

在 hello StorSimple 裝置刀鋒視窗中，您會看到 hello 選項來管理您的 StorSimple 裝置。 您可以看到 hello 的上方 hello 刀鋒視窗和 hello 左邊 hello 管理命令。 使用這些選項 tooadd 共用或磁碟區，或更新，或容錯移轉您的裝置。

![管理命令列](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>基本資訊

hello essentials 區域會擷取一些 hello 重要屬性，例如、 hello 狀態、 模型、 目標 IQN 和 hello 軟體版本。 

![裝置的基本資訊](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>監視

* hello**警示**磚提供了您的裝置，依警示嚴重性分組之所有 hello 作用中警示的快照集。

    ![警示圖格](./media/storsimple-8000-device-dashboard/device-summary4.png)

    按一下 hello 磚 tooopen hello**警示**刀鋒視窗，然後按一下個別警示 tooview 其他詳細資料的警示，包括任何建議的動作。 如果 hello 問題已經解決，您也可以清除 hello 警示。

    ![按一下 [警示] 圖格](./media/storsimple-8000-device-dashboard/device-summary10.png)

* hello**狀態和健全狀況**磚提供了深入了解 hello 硬體元件健全狀況之裝置，包括 hello 裝置狀態。 hello 裝置狀態可能是離線、 線上、 停用，或準備 tooset up。

    ![狀態與健康情況圖格](./media/storsimple-8000-device-dashboard/device-summary5.png)

* hello**磁碟區**磚都可讓您依狀態分組的裝置中的磁碟區的 hello 數目的摘要。

    ![磁碟區圖格](./media/storsimple-8000-device-dashboard/device-summary6.png)

    按一下 hello 磚 tooopen hello**磁碟區**清單刀鋒視窗中，然後按一下個別磁碟區 tooview 或修改其屬性。
    
    ![按一下 [磁碟區] 圖格](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    如需詳細資訊，請參閱如何太[管理磁碟區](storsimple-8000-manage-volumes-u2.md)。

* 在 hello**使用量**圖表中，您可以檢視 hello 跨您的裝置，並耗用 hello 過去 7 天，hello 預設時間週期的 hello 雲端存放裝置使用的主要儲存體。

     ![使用量圖格](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose 不同的時間刻度，使用 hello**編輯**hello 右上角中的 hello 圖表的選項。

     ![編輯使用量圖表](./media/storsimple-8000-device-dashboard/device-summary12.png)

     在此圖中，您可以檢視度量 hello 總主要儲存體 （hello 由主機 tooyour 裝置寫入的資料量） 並 hello 總雲端經過一段時間的裝置所使用的存放裝置。
  
     在此內容中*主要儲存體*參照 toohello 總量 hello 主機寫入的資料，並可依磁碟區類型細分：*主要的階層式儲存體*同時包含在本機儲存資料和資料階層式的 toohello 雲端。 「主要本機釘選儲存體」只包含在本機儲存的資料。 *雲端儲存體*，在 hello 相反，是 hello 的 hello 雲端中儲存的資料量總計的度量單位。 此儲存體包括分層式資料和備份。 hello hello 雲端中儲存的資料是重複資料刪除和壓縮，而主要儲存體指出 hello hello 資料重複資料刪除，且壓縮之前使用的儲存體的數量。 （您可以比較這些兩個數字 tooget hello 壓縮率的了解）。這兩個主要部署和雲端儲存體，hello 所示的金額為基礎 hello 追蹤您所設定的頻率。 例如，如果您選擇一週頻率，然後 hello 圖表可顯示資料中每一天 hello 前一週。

     一段時間，請選取 hello 耗用的雲端儲存體 toosee hello 數量**CLOUD STORAGE USED**選項。 toosee hello 總儲存體已寫入 hello 主機上，選取 hello **PRIMARY 分層 STORAGE USED**和**主要在本機固定的儲存體使用**選項。 
     如需詳細資訊，請參閱[使用 hello StorSimple 裝置管理員服務 toomonitor StorSimple 裝置](storsimple-monitor-device.md)。


* hello**容量**磚顯示 hello 主要儲存體佈建和跨 hello 裝置相對 toohello 可用總儲存體的剩餘 hello 相同。 **佈建**參考完成準備並配置供使用，儲存體的 toohello 數量**剩餘**參考 toohello 剩餘可以透過此裝置佈建的容量。 

    ![使用量圖格](./media/storsimple-8000-device-dashboard/device-summary8.png)

    按一下這個 hello 容量如何佈建階層式和本機固定磁碟區上的磚 tooview。 hello**剩餘分層**容量是 hello 可以包括雲端，同時 hello 佈建的可用容量**剩餘本機**是 hello 磁碟上剩餘的 hello 容量附加 toothis 裝置。

    ![按一下 [使用量] 圖表](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>後續步驟
* 深入了解 hello [StorSimple 服務摘要 刀鋒視窗](storsimple-8000-service-dashboard.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。

