---
title: "aaaManage 您 StorSimple 備份目錄 |Microsoft 文件"
description: "說明如何 toouse hello StorSimple Manager 服務備份類別目錄 頁面 toolist，選取，並刪除磁碟區的備份組。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a>使用 hello StorSimple Manager 服務 toomanage 備份類別目錄
## <a name="overview"></a>概觀
StorSimple Manager 服務的 hello**備份類別目錄**頁面會顯示所有手動或排程備份時，會建立 hello 備份組。 您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。

本教學課程說明如何 toolist、 select 和刪除的備份組。 toolearn 如何 toorestore 從備份裝置跳過[從備份集還原您的裝置](storsimple-restore-from-backup-set.md)。 如何 tooclone 磁碟區，跳過 toolearn[複製 StorSimple 磁碟區](storsimple-clone-volume.md)。

![備份類別目錄](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

hello**備份類別目錄**頁面會提供查詢 toonarrow 備份組的選取項目。 您可以篩選 hello 備份組所擷取，根據下列參數的 hello:

* **裝置**– hello 裝置的 hello 當初建立備份組。
* **備份原則或磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。
* **From 和 To** – hello hello 備份集建立時的日期和時間範圍。

hello 篩選的備份組會再製成資料表根據 hello 下列屬性：

* **名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。
* **大小**– hello hello 備份組的實際大小。
* **建立日期**– hello 日期和建立 hello 備份時的時間。 
* **類型** - 備份組可以是本機快照集或雲端快照集。 本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。 本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。
* **起始者**– 由排程或手動使用者 hello 備份也可以自動初始化。 您可以使用備份原則 tooschedule 備份。 或者，您可以使用 hello**取得備份**選項 tootake 手動備份。

## <a name="list-backup-sets-for-a-volume"></a>列出磁碟區的備份組
完成下列步驟 toolist hello 所有 hello 備份磁碟區。

#### <a name="toolist-backup-sets"></a>toolist 備份組
1. 在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。
2. 篩選 hello 選取項目，如下所示：
   
   1. 選取 hello 適當的裝置。
   2. 在 [hello] 下拉式清單中，選擇磁碟區 tooview hello 對應 hello 備份。
   3. 指定 hello 時間範圍。
   4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute 此查詢。
      
      備份組的 hello 清單應會顯示 hello 與 hello 選取磁碟區相關聯的備份。

## <a name="select-a-backup-set"></a>選取備份組
完成下列步驟 tooselect 的備份組的磁碟區或備份原則的 hello。

#### <a name="tooselect-a-backup-set"></a>tooselect 備份組
1. 在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。
2. 篩選 hello 選取項目，如下所示：
   
   1. 選取 hello 適當的裝置。
   2. 在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。
   3. 指定 hello 時間範圍。
   4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute 此查詢。
      
      hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。
3. 選取並展開備份組。 hello**還原**和**刪除**選項會顯示在 hello hello 頁面的底部。 您可以執行這些動作 hello 您選取的備份組。

## <a name="delete-a-backup-set"></a>刪除備份組
當您不再想與它相關聯的 tooretain hello 資料刪除的備份。 執行下列步驟 toodelete 備份組的 hello。

#### <a name="toodelete-a-backup-set"></a>toodelete 備份組
1. 在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄] 索引標籤**。
2. 篩選 hello 選取項目，如下所示：
   
   1. 選取 hello 適當的裝置。
   2. 在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。
   3. 指定 hello 時間範圍。
   4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) tooexecute 此查詢。
      
      hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。
3. 選取並展開備份組。 hello**還原**和**刪除**選項會顯示在 hello hello 頁面的底部。 按一下 [刪除] 。
4. 當 hello 刪除正在進行時和順利完成時，系統會通知您。 Hello 刪除完成之後，重新整理此頁面上的 hello 查詢。 hello 刪除備份組不會再出現在 hello 清單中的備份組。

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello 備份類別目錄 toorestore 您的裝置，從備份集](storsimple-restore-from-backup-set.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

