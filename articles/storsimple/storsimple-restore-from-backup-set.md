---
title: "從備份還原 StorSimple 磁碟區 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 的 [備份類別目錄] 頁面，從備份組還原 StorSimple 磁碟區。"
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
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>從備份組還原 StorSimple 磁碟區
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Overview
[備份類別目錄]  頁面會顯示在產生手動或自動備份時建立的所有備份組。 您可以使用此頁面來列出備份原則或磁碟區的所有備份、選取或刪除備份，或是使用備份來還原或複製磁碟區。

 ![備份類別目錄頁面](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

本教學課程說明如何使用 [備份資料目錄]  頁面，從備份組還原您裝置上的磁碟區。

## <a name="how-to-use-the-backup-catalog"></a>如何使用備份類別目錄
[備份類別目錄]  頁面提供查詢，可協助您縮小備份組選取範圍。 您可以篩選根據下列參數擷取的備份組：

* **裝置** - 建立備份組所在的裝置。
* **備份原則**或**磁碟區** – 與此備份組相關聯的備份原則或磁碟區。
* **起****迄** – 建立備份組的日期和時間範圍。

接著會根據下列屬性，將篩選的備份組列表顯示：

* **名稱** - 與備份組相關聯的備份原則或磁碟區的名稱。
* **大小** - 備份組的實際大小。
* **建立日期** - 建立備份的日期和時間。 
* **類型** - 備份組可以是本機快照集或雲端快照集。 本機快照是本機儲存於裝置上的所有磁碟區資料備份，而雲端快照是指位於雲端的磁碟區資料備份。 本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。
* **起始者** - 備份可根據排程自動初始，或由使用者手動初始。 (您可以使用備份原則來排程備份。 或者，可以使用 [取得備份] 選項來取得互動式備份。)

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a>如何從備份還原您的 StorSimple 磁碟區
您可以使用 [備份類別目錄]  頁面，從特定的備份還原 StorSimple 磁碟區。 

> [!WARNING]
> 從備份還原將從備份取代現有的磁碟區。 這可能會造成在取得備份之後寫入的所有資料遺失。
> 
> 

在磁碟區上起始還原之前，請確定磁碟區已離線。 您必須先讓主機上的磁碟區離線，再讓裝置離線。 請遵循 [使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)中的步驟進行。 執行下列步驟，以從備份組還原磁碟區。

### <a name="to-restore-from-a-backup-set"></a>從備份組還原
1. 在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤。
   
    ![備份類別目錄](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. 選取備份組，如下所示：
   
   1. 選取適當的裝置。
   2. 在下拉式清單中，針對要選取的備份選擇磁碟區或備份原則。
   3. 指定時間範圍。
   4. 按一下核取圖示  ![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) 以執行此查詢。
      
      與選取的磁碟區或備份原則相關聯的備份應該會出現在備份組清單中。
3. 展開備份組以檢視相關聯的磁碟區。 您必須先在主機和裝置上將這些磁碟區離線，才能還原它們。 請遵循 [使磁碟區離線](storsimple-manage-volumes.md#take-a-volume-offline)中的步驟進行。
   
   > [!IMPORTANT]
   > 確定您已先讓主機上的磁碟區離線，然後再讓裝置上的磁碟區離線。 如果您並未讓主機上的磁碟區離線，可能會導致資料損毀。
   > 
   > 
4. 選取備份組。 按一下頁面底部的 [還原]  。
5. 系統將提示您進行確認。 
   
    ![確認電子郵件](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. 檢閱還原資訊，然後按一下核取圖示 ![核取圖示](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png)中的步驟進行。 這將會初始還原工作，而您可以藉由存取 [工作]  頁面來進行檢視。 
7. 還原完成之後，您可以確認磁碟區的內容已由備份的磁碟區所取代。

![提供的影片](./media/storsimple-restore-from-backup-set/Video_icon.png) **提供的影片**

若要觀看影片示範如何使用 StorSimple 的複製和還原功能，將已刪除的檔案復原，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。

## <a name="next-steps"></a>後續步驟
* 了解如何 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。
* 了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。

