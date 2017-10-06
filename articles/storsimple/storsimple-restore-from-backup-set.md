---
title: "aaaRestore StorSimple 磁碟區從備份 |Microsoft 文件"
description: "說明如何 toouse 會 hello StorSimple Manager 服務備份類別目錄 頁面 toorestore StorSimple 磁碟區從備份組。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>從備份組還原 StorSimple 磁碟區
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>概觀
hello**備份類別目錄**頁面會顯示所有 hello 的備份組時手動或自動備份所建立的。 您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。

 ![備份類別目錄頁面](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

本教學課程說明如何 toouse hello**備份類別目錄**頁面 toorestore 備份組中的裝置上的磁碟區。

## <a name="how-toouse-hello-backup-catalog"></a>如何 toouse hello 備份類別目錄
hello**備份類別目錄**頁面會提供可協助您 toonarrow 查詢您的備份組選項。 您可以篩選 hello 的備份組會擷取根據 hello 下列參數：

* **裝置**– hello 裝置的 hello 當初建立備份組。
* **備份原則**或**磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。
* **從**和**至**– hello hello 備份集建立時的日期和時間範圍。

hello 篩選的備份組會再製成資料表根據 hello 下列屬性：

* **名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。
* **大小**– hello hello 備份組的實際大小。
* **在建立**– hello 日期和建立 hello 備份時的時間。 
* **類型** - 備份組可以是本機快照集或雲端快照集。 本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。 本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。
* **由起始**– hello 備份可以自動根據 tooa 排程起始或由使用者手動。 （您可以使用備份原則 tooschedule 備份。 或者，您可以使用 hello**取得備份**選項 tootake 互動式備份。)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>如何 toorestore 您的 StorSimple 磁碟區從備份
您可以使用 hello**備份類別目錄**頁面 toorestore 您的 StorSimple 磁碟區，從特定的備份。 

> [!WARNING]
> 從備份還原，將會取代 hello hello 備份中的現有磁碟區。 這也可能造成 hello hello 備份後寫入任何資料遺失。
> 
> 

初始化磁碟區上的還原之前，請確定 hello 磁碟區已離線。 您將需要 tootake hello 上的磁碟區離線 hello 主機第一次，然後 hello 裝置。 中的 hello 步驟[使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)。 執行下列步驟 toorestore 磁碟區從備份組的 hello。

### <a name="toorestore-from-a-backup-set"></a>從備份集 toorestore
1. 在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。
   
    ![備份類別目錄](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. 選取備份組，如下所示：
   
   1. 選取 hello 適當的裝置。
   2. 在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。
   3. 指定 hello 時間範圍。
   4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) tooexecute 此查詢。
      
      hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。
3. 展開 hello 備份組 tooview hello 相關聯的磁碟區。 這些磁碟區必須採取 hello 主機和裝置上離線再進行還原。 中的 hello 步驟[使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)。
   
   > [!IMPORTANT]
   > 請確定您已經執行 hello 磁碟區離線 hello 主機上的第一次之後您才能 hello 裝置上的 hello 磁碟區離線。 如果您不會在 hello 主機上取得 hello 磁碟區離線，有可能導致 toodata 損毀。
   > 
   > 
4. 選取備份組。 按一下**還原**hello hello 頁底端。
5. 系統將提示您進行確認。 
   
    ![確認電子郵件](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. 檢閱 hello 還原資訊，然後按一下核取圖示，hello![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png)。 這會起始的還原作業，您可以藉由存取 hello 檢視**作業**頁面。 
7. Hello 還原完成後，您可以確認您的磁碟區 hello 內容會取代從 hello 備份的磁碟區。

![提供的影片](./media/storsimple-restore-from-backup-set/Video_icon.png) **提供的影片**

toowatch 的影片示範如何使用 hello 複製和還原功能在 StorSimple toorecover 刪除檔案中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

