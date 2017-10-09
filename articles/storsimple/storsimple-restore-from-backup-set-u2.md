---
title: "aaaRestore StorSimple 磁碟區從備份 |Microsoft 文件"
description: "說明如何 toouse 會 hello StorSimple Manager 服務備份類別目錄 頁面 toorestore StorSimple 磁碟區從備份組。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>從備份組還原 StorSimple 磁碟區 (Update 2)
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>概觀
hello**備份類別目錄**頁面會顯示所有 hello 的備份組時手動或自動備份所建立的。 使用此頁面 toolist 和管理備份、 備份組，從還原或複製磁碟區。

 ![備份類別目錄頁面](./media/storsimple-restore-from-backup-set-u2/restore.png)

本教學課程說明如何 toouse hello**備份類別目錄**頁面 toorestore 備份組中的裝置。

您可以從本機或雲端備份還原磁碟區。 在任一情況下，hello 還原作業會立即在 hello 背景中下載的資料時，才帶 hello 區上線。 

## <a name="before-you-restore"></a>還原之前
起始還原作業之前，您應該留意下列注意事項 hello:

* **Hello 磁碟區離線**– 採取 hello 磁碟區離線，這兩個 hello 主機上並 hello 裝置，才能起始 hello 還原作業。 雖然 hello 還原作業會自動帶出 hello 裝置上的 hello 區上線，您必須手動讓 hello 裝置上線 hello 主機上。 Hello 磁碟區上線 hello 裝置上時，您可以將磁碟 hello 區帶入 hello 主機上。 （您不需要 toowait hello 還原作業完成之前。）程序，跳過[使磁碟區離線](storsimple-manage-volumes-u2.md#take-a-volume-offline)。
* **還原後的磁碟區類型**– 根據 hello 快照中的 hello 類型還原已刪除磁碟區。 已固定在本機的磁碟區會還原為固定在本機的磁碟區，而已分層的磁碟區會還原為階層式磁碟區。
  
    現有的磁碟區，hello 目前使用的磁碟區類型 hello 會覆寫儲存 hello 快照中的 hello 型別。 比方說，如果您從 hello 磁碟區類型的階層時擷取的快照集還原的磁碟區和，磁碟區類型現在是在本機釘選 （因為 tooa 轉換作業），然後 hello 磁碟區會還原為本機固定磁碟區。 同樣地，如果擴充現有本機固定磁碟區，並且從較舊的快照時 hello 的磁碟區是較小採取後續還原，hello 還原磁碟區會保留 hello 目前擴充的大小。
  
    您無法從階層式磁碟區 tooa 固定在本機磁碟區轉換磁碟區或_反之亦然_時正在還原 hello 磁碟區。 等候 hello 還原作業已完成，然後將轉換 hello 磁碟區 tooanother 類型。 如需轉換磁碟區資訊，請移太[變更 hello 磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。 
* **hello 磁碟區大小會反映在 hello 還原磁碟區**– 這是一項重要的考量，如果您要還原已刪除，（因為完整佈建本機固定磁碟區） 的本機固定磁碟區。 請確定您有足夠的空間，然後再嘗試 toorestore 之前已刪除本機固定磁碟區。 
* **正在還原時，您無法展開磁碟區**– 等候 hello 還原作業完成之前嘗試 tooexpand hello 磁碟區。 如需擴充磁碟區資訊，請移太[修改磁碟區](storsimple-manage-volumes-u2.md#modify-a-volume)。
* **您可以執行備份，而您要還原的本機磁碟區**– 如程序，請移過[使用 hello StorSimple Manager 服務 toomanage 備份原則](storsimple-manage-backup-policies.md)。
* **您可以取消的還原作業**– 如果您取消 hello 還原作業，然後 hello 磁碟區會回復 toohello 起始 hello 還原之前的狀態。 程序，跳過[取消工作](storsimple-manage-jobs-u2.md#cancel-a-job)。

## <a name="how-does-restore-work"></a>還原的運作方式
如果是執行 Update 4 或更新版本的裝置，就會實作熱度圖式還原。 Hello 主機要求 tooaccess 資料達到 hello 裝置，這些要求追蹤，並且建立 heatmap。 要求率高會導致與更高的熱資料區塊，而較低的要求率轉譯 toochunks 與較低的熱度。 您必須存取 hello 資料至少兩次 toobe 標示為_熱_。 已修改的檔案也會標示為「熱」。 一旦您起始 hello 還原，接著會根據 hello heatmap 主動式凍結的資料。 版本早於 Update 4 hello 已下載資料根據存取只還原期間。 

熱度圖式追蹤只會針對階層式磁碟區啟用，而不支援固定在本機的磁碟區。 Heatmap 還原也不支援在複製磁碟區 tooanother 裝置時。 如果沒有就地還原 hello 磁碟區 toobe 還原的本機快照集存在 hello 裝置上，然後我們不要不解除凍結 （如資料在本機已可用）。 根據預設，當您還原，hello 解除凍結作業不會起始，主動解除凍結 hello heatmap 為基礎的資料。 在更新 4 中，Windows PowerShell cmdlet 可以是使用的 tooquery 執行解除凍結工作、 取消解除凍結工作，並取得 hello hello 解除凍結工作狀態。

* `Get-HcsRehydrationJob`-此 cmdlet 會取得 hello hello 解除凍結工作狀態。 單一解除凍結作業會針對某一個磁碟區來觸發。
* `Set-HcsRehydrationJob`-此 cmdlet 可讓您 toopause、 停止、 繼續 hello 解除凍結工作，當 hello 解除凍結正在進行中。 

如需有關解除凍結 cmdlet 的詳細資訊，請移太[Windows PowerShell for StorSimple 的 cmdlet 參考](https://technet.microsoft.com/library/dn688168.aspx)。

透過自動解除凍結功能，通常可預期較高的暫時性讀取效能。 hello 實際 magniutde 改良功能取決於各種因素，例如存取模式、 資料變換量，以及資料類型。 toocancel 解除凍結工作，您可以使用 hello PowerShell cmdlet。 如果您希望所有的 hello 未來還原 toopermanently 停用解除凍結工作，請連絡 Microsoft 支援服務。

## <a name="how-toouse-hello-backup-catalog"></a>如何 toouse hello 備份類別目錄
hello**備份類別目錄**頁面會提供可協助您 toonarrow 查詢您的備份組選項。 您可以篩選 hello 的備份組會擷取根據 hello 下列參數：

* **裝置**– hello 裝置的 hello 當初建立備份組。
* **備份原則**或**磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。
* **從**和**至**– hello hello 備份集建立時的日期和時間範圍。

hello 篩選的備份組會再製成資料表根據 hello 下列屬性：

* **名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。
* **大小**– hello hello 備份組的實際大小。
* **在建立**– hello 日期和建立 hello 備份時的時間。 
* **類型** - 備份組可以是本機快照集或雲端快照集。 本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份。 雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。 本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。
* **由起始**– hello 備份可以自動根據 tooa 排程起始或由您手動。 （您可以使用備份原則 tooschedule 備份。 或者，您可以使用 hello**取得備份**選項 tootake 互動式備份。)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>如何 toorestore 您的 StorSimple 磁碟區從備份
您可以使用 hello**備份類別目錄**頁面 toorestore 您的 StorSimple 磁碟區，從特定的備份。 請記住，不過，還原磁碟區還原 hello hello 備份時的磁碟區 toohello 狀態。 Hello 備份作業後，新增任何資料都會遺失。

> [!WARNING]
> 從備份還原時，會取代 hello hello 備份中的現有磁碟區。 這也可能造成 hello hello 備份後寫入任何資料遺失。
> 
> 

### <a name="toorestore-your-volume"></a>toorestore 您的磁碟區
1. 在 hello StorSimple Manager 服務頁面上，按一下 [hello**備份類別目錄**] 索引標籤。
   
    ![備份類別目錄](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. 選取備份組，如下所示：
   
   1. 選取 hello 適當的裝置。
   2. 在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。
   3. 指定 hello 時間範圍。
   4. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute 此查詢。
      
      hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。
3. 展開 hello 備份組 tooview hello 相關聯的磁碟區。 這些磁碟區必須採取 hello 主機和裝置上離線再進行還原。 存取 hello 磁碟區上 hello**磁碟區容器**頁面，然後再依照中的 hello 步驟[使磁碟區離線](storsimple-manage-volumes-u2.md#take-a-volume-offline)tootake 離線。
   
   > [!IMPORTANT]
   > 請確定您已經執行 hello 磁碟區離線 hello 主機上的第一次之後您才能 hello 裝置上的 hello 磁碟區離線。 如果您不會在 hello 主機上取得 hello 磁碟區離線，有可能導致 toodata 損毀。
   > 
   > 
4. 瀏覽後 toohello**備份類別目錄**索引標籤並選取備份組。
5. 按一下**還原**hello hello 頁底端。
6. 系統會提示您進行確認。 檢閱 hello 還原的詳細資訊，，然後選取 hello 確認核取方塊。
   
    ![確認電子郵件](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. 按一下核取圖示，hello![核取圖示](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png)。 還原作業開始。 您可以藉由存取 hello 檢視 hello 作業**作業**頁面。 
8. Hello 還原完成後，您可以確認您的磁碟區 hello 內容會取代從 hello 備份的磁碟區。

![提供的影片](./media/storsimple-restore-from-backup-set-u2/Video_icon.png) **提供的影片**

toowatch 的影片示範如何使用 hello 複製和還原功能在 StorSimple toorecover 刪除檔案中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。

## <a name="if-hello-restore-fails"></a>如果 hello 還原失敗
如果 hello 還原作業將會失敗，因為任何原因，您會收到警示。 如果發生這種情況，hello 備份的重新整理 hello 備份清單 tooverify 為仍然有效。 如果 hello 備份有效，且您從 hello 雲端還原，然後連線問題可能導致 hello 問題。 

toocomplete hello 還原作業，hello 主機上讓 hello 磁碟區離線，然後重試 hello 還原作業。 Hello 還原程序期間所執行的任何修改 toohello 磁碟區資料會遺失。

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理 StorSimple 磁碟區](storsimple-manage-volumes-u2.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

