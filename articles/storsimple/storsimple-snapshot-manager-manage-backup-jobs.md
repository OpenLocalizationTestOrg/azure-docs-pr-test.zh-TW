---
title: "aaaStorSimple Snapshot Manager 備份工作 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooview 及管理排程、 目前執行中和已完成的備份工作。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a>使用 StorSimple Snapshot Manager tooview 及管理備份工作

## <a name="overview"></a>概觀
hello**作業**節點 hello**範圍** 窗格會顯示 hello**排程**，**過去 24 小時**，和**執行**的備份工作，您起始了以互動方式或依據設定的原則。 

本教學課程說明如何使用 hello**作業**節點 toodisplay 資訊已排程、 最近，和目前執行的備份工作。 (hello 清單作業和對應的資訊會出現在 hello**結果**窗格。)此外，您也可以以滑鼠右鍵按一下列出的作業，並查看內容功能表，其中列出可用的動作。

## <a name="view-scheduled-jobs"></a>檢視已排程的作業
使用下列程序 tooview 的 hello 排定的備份工作。

#### <a name="tooview-scheduled-jobs"></a>tooview 排程工作
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。 
2. 在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後按一下**排程**。 hello 下列資訊會出現在 hello**結果**窗格：
   
   * **名稱**– hello hello 排定之快照的名稱
   * **接下來執行**– hello 的日期和時間 hello 下一個排程的快照集
   * **上次執行**– hello 的日期和時間 hello 最新的排程快照集
     
     > [!NOTE]
     > 僅一次快照，如 hello **下次執行**和**上次執行**將 hello 相同。
     
     ![排定的備份工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. tooperform 其他動作的特定作業，以滑鼠右鍵按一下 hello 工作名稱在 hello**結果**窗格，然後選取從 hello 功能表選項。

## <a name="view-recent-jobs"></a>檢視最近的作業
使用下列程序 tooview 備份 hello 和還原作業中完成之 hello 過去 24 小時。

#### <a name="tooview-recent-jobs"></a>tooview 最近工作
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後按一下**過去 24 小時**。 hello**結果** 窗格會顯示備份作業的 hello 過去 24 小時 （tooa 最多 64 個工作中）。 hello 下列資訊會出現在 hello**結果** 窗格中的，根據 hello**檢視**您指定的選項：
   
   * **名稱**– hello hello 排定之快照的名稱。
   * **啟動**– hello 開始日期和時間時 hello 快照集。
   * **停止**– hello 或日期和時間時 hello 快照集完成已終止。
   * **經過**– hello 一段時間之間 hello**已啟動**和**已停止**時間。
   * **狀態**– hello hello 最近完成的作業的狀態。 **成功**指出該 hello 備份已成功建立。 **無法**指出 hello 工作執行成功。
   * **資訊**– hello hello 失敗原因。
   * **已處理的位元組 (MB)** – hello 數量 （以 mb 為單位） 已處理的 hello 磁碟區群組中的資料。 
     
     ![執行在 hello 過去 24 小時內的工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. tooperform 其他動作的特定作業，以滑鼠右鍵按一下 hello 工作名稱在 hello**結果**窗格，然後選取從 hello 功能表選項。
   
    ![刪除工作](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a>檢視目前執行中的作業
使用下列程序 tooview 作業目前正在執行的 hello。

#### <a name="tooview-currently-running-jobs"></a>tooview 目前執行的工作
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後按一下**執行**。 根據 hello**檢視**選項指定，hello 下列資訊會出現在 hello**結果**窗格：
   
   * **名稱**– hello hello 排定之快照的名稱。
   * **啟動**– hello 開始日期和時間時 hello 快照集。
   * **檢查點**– hello 的 hello 備份目前的動作。
   * **狀態**– hello 完成百分比。
   * **經過**– hello hello 備份開始後經過的時間量。 
   * **平均輸送量 (MB)** – 處理 (MBs) 所花費的時間總計的資料處理 toothat 的位元組總數的比率。
   * **處理的位元組 (MB)** – 處理的總資料位元組 (以 MB 為單位)。
   * **寫入的位元組 (MB)** – 寫入的總資料位元組 (以 MB 為單位)。 它包含 hello 資料以及 hello 中繼資料，並因此大於通常 hello 處理的位元組。
     
     ![目前執行中的工作](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. tooperform 其他動作的特定作業，以滑鼠右鍵按一下 hello 工作名稱在 hello**結果**窗格，然後選取從 hello 功能表選項。

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 了解如何太[使用 StorSimple Snapshot Manager toomanage hello 備份類別目錄](storsimple-snapshot-manager-manage-backup-catalog.md)。

