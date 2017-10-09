---
title: "aaaManage 您 StorSimple 備份目錄 |Microsoft 文件"
description: "說明如何 toouse hello StorSimple 裝置管理員服務備份類別目錄 頁面 toolist 選取，並刪除備份組。"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a>使用 hello StorSimple 裝置管理員服務 toomanage 備份類別目錄
## <a name="overview"></a>概觀
hello StorSimple 裝置管理員服務**備份類別目錄**刀鋒視窗會顯示所有手動或排程備份時，會建立 hello 備份組。 您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。

本教學課程說明如何 toolist、 select 和刪除的備份組。 toolearn 如何 toorestore 從備份裝置跳過[從備份集還原您的裝置](storsimple-8000-restore-from-backup-set-u2.md)。 如何 tooclone 磁碟區，跳過 toolearn[複製 StorSimple 磁碟區](storsimple-8000-clone-volume-u2.md)。

![備份類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

hello**備份類別目錄**刀鋒視窗中提供的查詢 toonarrow 備份組的選取項目。 您可以篩選 hello 備份組所擷取，根據下列參數的 hello:

* **裝置**– hello 裝置的 hello 當初建立備份組。
* **備份原則或磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。
* **From 和 To** – hello hello 備份集建立時的日期和時間範圍。

hello 篩選的備份組會再製成資料表根據 hello 下列屬性：

* **名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。
* **大小**– hello hello 備份組的實際大小。
* **建立日期**– hello 日期和建立 hello 備份時的時間。 
* **類型** - 備份組可以是本機快照集或雲端快照集。 本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。 本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。
* **起始者**– 由排程或手動使用者 hello 備份也可以自動初始化。 您可以使用備份原則 tooschedule 備份。 或者，您可以使用 hello**取得備份**選項 tootake 手動備份。

## <a name="list-backup-sets-for-a-backup-policy"></a>列出備份原則的備份組
完成下列步驟 toolist hello 所有 hello 備份的備份原則。

#### <a name="toolist-backup-sets"></a>toolist 備份組
1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**備份類別目錄**。

2. 篩選 hello 選取項目，如下所示：
   
   1. 指定 hello 時間範圍。
   2. 選取 hello 適當的裝置。
   3. 依篩選**備份原則**tooview hello 對應 hello 備份。
   3. 從 hello 備份原則下拉式清單中，選擇 **所有**tooview 所有 hello 上 hello 選取備份裝置。
   4. 按一下**套用**tooexecute 此查詢。
      
      備份組的 hello 清單應會顯示 hello 與 hello 選取備份原則相關聯的備份。

      ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a>選取備份組
完成下列步驟 tooselect 的備份組的磁碟區或備份原則的 hello。

#### <a name="tooselect-a-backup-set"></a>tooselect 備份組
1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**備份類別目錄**。
2. 篩選 hello 選取項目，如下所示：
   
   1. 指定 hello 時間範圍。 
   2. 選取 hello 適當的裝置。 
   3. 篩選您想 tooselect hello 備份的磁碟區或備份原則。
   4. 按一下**套用**tooexecute 此查詢。
      
      hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。

      ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. 選取並展開備份組。 您現在可以看到 hello 切分 hello 它所包含的磁碟區的備份組。 hello**還原**和**刪除**選項都是透過 hello 備份組的 hello 操作功能表 （按一下滑鼠右鍵）。 您可以執行這些動作 hello 您選取的備份組。

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a>刪除備份組
當您不再想與它相關聯的 tooretain hello 資料刪除的備份。 執行下列步驟 toodelete 備份組的 hello。

#### <a name="toodelete-a-backup-set"></a>toodelete 備份組
 移 tooyour StorSimple 裝置管理員服務，然後按一下**備份類別目錄**。
2. 篩選 hello 選取項目，如下所示：
   
   1. 指定 hello 時間範圍。 
   2. 選取 hello 適當的裝置。 
   3. 篩選您想 tooselect hello 備份的磁碟區或備份原則。
   4. 按一下**套用**tooexecute 此查詢。
      
      hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。

      ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. 選取並展開備份組。 您現在可以看到 hello 切分 hello 它所包含的磁碟區的備份組。 hello**還原**和**刪除**選項都是透過 hello 備份組的 hello 操作功能表 （按一下滑鼠右鍵）。 以滑鼠右鍵按一下選取的 hello 備份組，然後從 hello 內容功能表中，選取**刪除**。

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. 當提示確認，請檢閱 hello 顯示資訊，然後按一下**刪除**。 會永久刪除 hello 所選的備份。

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. 當 hello 刪除正在進行時和順利完成時，系統會通知您。 Hello 刪除完成之後，重新整理此頁面上的 hello 查詢。 hello 刪除備份組不會再出現在 hello 清單中的備份組。

    ![移 toobackup 類別目錄](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 hello 備份類別目錄 toorestore 您的裝置，從備份集](storsimple-8000-restore-from-backup-set-u2.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

