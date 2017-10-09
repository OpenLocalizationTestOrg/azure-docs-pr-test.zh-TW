---
title: "aaaMicrosoft Azure StorSimple Virtual Array 備份教學課程 |Microsoft 文件"
description: "描述如何設定 StorSimple Virtual Array tooback 共用和磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a>備份 StorSimple Virtual Array 上的共用或磁碟區

## <a name="overview"></a>概觀

hello StorSimple Virtual Array 是混合式雲端儲存體在內部部署虛擬裝置，可以設定為檔案伺服器或 iSCSI 伺服器。 hello 虛擬陣列允許 hello 使用者 toocreate 所有 hello 共用或磁碟區備份的排程和手動備份 hello 裝置上。 設為檔案伺服器時，也可進行項目層級的復原。 本教學課程描述如何排程 toocreate 和手動備份，並執行項目層級復原 toorestore 已刪除的檔案，您的虛擬陣列上。

本教學課程適用於 toohello StorSimple 虛擬陣列只。 如 8000 系列的相關資訊，請移至太[建立 8000 系列裝置的備份](storsimple-manage-backup-policies-u2.md)

## <a name="back-up-shares-and-volumes"></a>備份共用和磁碟區

備份可提供共用和磁碟區的時間點保護、改善復原能力，同時讓還原時間降至最低。 您有兩種方法可以備份 StorSimple 裝置上的共用或磁碟區：「排程」或「手動」。 每個 hello 方法 hello 下列各節中討論。

## <a name="change-hello-backup-start-time"></a>變更 hello 備份開始時間

> [!NOTE]
> 此版本中，在排定的備份會建立預設原則，每天在指定的時間執行，而且所有 hello 共用或磁碟區都備份 hello 裝置上。 它不是這一次可能 toocreate 自訂原則進行排定的備份。


您的 StorSimple Virtual Array 有預設的備份原則會在一天 (22:30) 的指定時間啟動和所有 hello 共用或磁碟區上都備份 hello 裝置一天一次。 您可以變更 hello hello 備份開始，但 hello 頻率和 hello （可指定備份 tooretain 的 hello 數目） 的保留，無法變更的時間。 在這些備份期間 hello 整個虛擬裝置會備份。 這可能會無法對於 hello 裝置 hello 效能的影響，而且會影響 hello 裝置上部署的 hello 工作負載。 因此，建議您將這些備份排定在離峰時段。

 toochange hello 預設備份開始時間，請執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)。

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a>toochange hello 的開始時間 hello 預設備份原則

1. 跳過**裝置**。 以您的 StorSimple 裝置 Manager 服務註冊的裝置 hello 清單隨即出現。 
   
    ![瀏覽 toodevices](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. 選取並按一下您的裝置。 hello**設定**刀鋒視窗會顯示。 跳過**管理 > 的備份原則**。
   
    ![選取您的裝置](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. 在 hello**的備份原則**刀鋒視窗中，hello 預設開始時間為 22:30。 您可以指定 hello 每日排程 hello 新開始時間，以裝置時區為準。
   
    ![瀏覽 toobackup 原則](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. 按一下 [儲存] 。

### <a name="take-a-manual-backup"></a>進行手動備份

此外 tooscheduled 備份，您可以進行裝置資料手動 （視需要） 備份在任何時間。

#### <a name="toocreate-a-manual-backup"></a>toocreate 手動備份

1. 跳過**裝置**。 選取您的裝置，然後以滑鼠右鍵按一下**...**在最右邊的 hello hello 選取的資料列中。 Hello 內容功能表中選取**取得備份**。
   
    ![瀏覽 tootake 備份](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. 在 hello**取得備份**刀鋒視窗中，按一下**取得備份**。 這將會備份所有 hello hello 檔案伺服器上的共用或 iSCSI 伺服器上的所有 hello 磁碟區。 
   
    ![正在啟動備份](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    依需求備份開始執行，您會看到備份作業已啟動。
   
    ![正在啟動備份](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    一旦 hello 工作順利完成之後，會通知您一次。 接著啟動 hello 備份程序。
   
    ![已建立備份工作](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. hello 備份及 hello 工作詳細資料，查看 tootrack hello 進度按一下 hello 通知。 這會帶您太**作業詳細資料**。
   
     ![備份作業詳細資料](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. Hello 備份完成之後，請移太**管理 > 備份類別目錄**。 在您的裝置上，您會看到所有 hello 共用 （或磁碟區） 的雲端快照。
   
    ![已完成的備份](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a>檢視現有的備份
tooview hello 現有的備份，執行下列步驟在 hello Azure 入口網站中的 hello。

#### <a name="tooview-existing-backups"></a>tooview 現有的備份

1. 跳過**裝置**刀鋒視窗。 選取並按一下您的裝置。 在 hello**設定**刀鋒視窗中，跳過**管理 > 備份類別目錄**。
   
    ![瀏覽 toobackup 類別目錄](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. 指定下列用於篩選的準則 toobe hello:
   
    - **時間範圍** – 可以是 [過去 1 小時]、[過去 24 小時]、[過去 7 天]、[過去 30 天]、[過去一年] 和 [自訂日期]。
    
    - **裝置**– 從檔案伺服器或與您的 StorSimple 裝置 Manager 服務登錄的 iSCSI 伺服器 hello 清單中選取。
   
    - **已起始** – 可以自動地 [已排程] \(依備份原則) 或 [手動] 起始 (由您執行)。
   
    ![篩選備份](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. 按一下 [Apply (套用)] 。 hello 篩選過的備份清單會顯示在 hello**備份類別目錄**刀鋒視窗。 請注意，永遠只會顯示 100 個備份項目。
   
    ![更新備份目錄](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a>後續步驟

深入了解 [administering your StorSimple Virtual Array (管理 StorSimple Virtual Array)](storsimple-ova-web-ui-admin.md)。

