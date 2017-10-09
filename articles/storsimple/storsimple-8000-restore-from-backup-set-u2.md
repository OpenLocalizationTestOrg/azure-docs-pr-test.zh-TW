---
title: "aaaRestore StorSimple 8000 系列的備份中的磁碟區 |Microsoft 文件"
description: "說明如何 toouse 會 hello StorSimple 裝置管理員服務備份類別目錄 toorestore StorSimple 磁碟區從備份組。"
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>從備份組還原 StorSimple 磁碟區

## <a name="overview"></a>概觀

本教學課程描述 hello 還原作業使用現有的備份組 StorSimple 8000 系列裝置上執行。 使用 hello**備份類別目錄**刀鋒視窗 toorestore 從本機磁碟區或雲端備份。 hello**備份類別目錄**刀鋒視窗會顯示所有 hello 的備份組時手動或自動備份所建立的。 hello 背景中下載資料時，立即 hello 從備份組的還原作業會顯示 hello 區上線。

替代方法 toostart 還原太 toogo**裝置 > [裝置] > 磁碟區**。 在 hello**磁碟區**刀鋒視窗中，選取磁碟區、 以滑鼠右鍵按一下 tooinvoke hello 操作功能表，然後選取**還原**。

## <a name="before-you-restore"></a>還原之前

在開始還原之前，檢閱下列注意事項 hello:

* **您必須讓 hello 磁碟區離線**– 採取 hello 磁碟區離線，這兩個 hello 主機上並 hello 裝置，才能起始 hello 還原作業。 雖然 hello 還原作業會自動帶出 hello 裝置上的 hello 區上線，您必須手動讓 hello 裝置上線 hello 主機上。 只要 hello 磁碟區已上線 hello 裝置上，您可以將磁碟 hello 區帶入 hello 主機上。 （您不需要 toowait hello 還原作業完成之前。）程序，跳過[使磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)。

* **還原後的磁碟區類型**– 還原已刪除磁碟區根據 hello 快照中的 hello 類型; 也就是已固定在本機的磁碟區就會還原為本機固定磁碟區並已分層的磁碟區就會還原為分層磁碟區。

    現有的磁碟區，hello 目前使用的磁碟區類型 hello 會覆寫儲存 hello 快照中的 hello 型別。 例如，如果您從 hello 磁碟區類型的階層時擷取的快照集還原的磁碟區，磁碟區類型現在是在本機固定的 （因為 tooa 轉換所執行的作業），然後 hello 磁碟區將會還原為本機固定磁碟區。 同樣地，如果現有本機固定磁碟區已展開，且後續從 hello 音量太短時，採取較舊的快照還原，hello 還原磁碟區將會保留 hello 目前擴充的大小。

    您無法將磁碟區轉換從階層式磁碟區 tooa 固定在本機磁碟區，或從本機固定磁碟區 tooa 分層磁碟區時正在還原 hello 磁碟區。 等候 hello 還原作業已完成，然後將轉換 hello 磁碟區 tooanother 類型。 如需轉換磁碟區資訊，請移太[變更 hello 磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。 

* **hello 磁碟區大小會反映在 hello 還原磁碟區**– 這是一項重要的考量，如果您要還原已刪除，（因為完整佈建本機固定磁碟區） 的本機固定磁碟區。 請確定您有足夠的空間，然後再嘗試 toorestore 之前已刪除本機固定磁碟區。

* **正在還原時，您無法展開磁碟區**– 等候 hello 還原作業完成之前嘗試 tooexpand hello 磁碟區。 如需擴充磁碟區資訊，請移太[修改磁碟區](storsimple-8000-manage-volumes-u2.md#modify-a-volume)。

* **還原本機磁碟區時，您可以執行備份**– 如程序，請移過[使用 hello StorSimple 裝置管理員服務 toomanage 備份原則](storsimple-8000-manage-backup-policies-u2.md)。

* **您可以取消的還原作業**– 如果您取消 hello 還原作業，然後 hello 磁碟區將會回復 toohello 起始 hello 還原作業之前的狀態。 程序，跳過[取消工作](storsimple-8000-manage-jobs-u2.md#cancel-a-job)。

## <a name="how-does-restore-work"></a>還原的運作方式

如果是執行 Update 4 或更新版本的裝置，就會實作熱度圖式還原。 Hello 主機要求 tooaccess 資料達到 hello 裝置，這些要求追蹤，並且建立 heatmap。 要求率高會導致與更高的熱資料區塊，而較低的要求率轉譯 toochunks 與較低的熱度。 您必須存取 hello 資料至少兩次 toobe 標示為_熱_。 已修改的檔案也會標示為「熱」。 一旦您起始 hello 還原，接著會根據 hello heatmap 主動式凍結的資料。 版本早於 Update 4 hello 被下載資料根據存取只還原期間。

下列注意事項 hello 套用 tooheatmap 基礎還原：

* 熱度圖追蹤只適用於階層式磁碟區，不支援固定在本機的磁碟區。

* 在複製磁碟區 tooanother 裝置時，不支援 Heatmap 還原。 

* 如果沒有就地還原 hello 磁碟區 toobe 還原的本機快照集存在 hello 裝置上，然後我們不要不解除凍結 （如資料在本機已可用）。 

* 根據預設，當您還原，hello 解除凍結作業不會起始，主動解除凍結 hello heatmap 為基礎的資料。 

在更新 4 中，Windows PowerShell cmdlet 可以是使用的 tooquery 執行解除凍結工作、 取消解除凍結工作，並取得 hello hello 解除凍結工作狀態。

* `Get-HcsRehydrationJob`-此 cmdlet 會取得 hello hello 解除凍結工作狀態。 單一解除凍結作業會針對某一個磁碟區來觸發。

* `Set-HcsRehydrationJob`-此 cmdlet 可讓您 toopause、 停止、 繼續 hello 解除凍結工作，當 hello 解除凍結正在進行中。

如需有關解除凍結 cmdlet 的詳細資訊，請移太[Windows PowerShell for StorSimple 的 cmdlet 參考](https://technet.microsoft.com/library/dn688168.aspx)。

透過自動解除凍結功能，通常可預期較高的暫時性讀取效能。 hello 實際 magniutde 改良功能取決於各種因素，例如存取模式、 資料變換量，以及資料類型。 

toocancel 解除凍結工作，您可以使用 hello PowerShell cmdlet。 如果您想 toopermanently 停用解除凍結工作的所有 hello 未來還原[連絡 Microsoft 支援服務](storsimple-8000-contact-microsoft-support.md)。

## <a name="how-toouse-hello-backup-catalog"></a>如何 toouse hello 備份類別目錄

hello**備份類別目錄**刀鋒視窗中提供的查詢，可協助您 toonarrow 備份組的選取項目。 您可以篩選 hello 的備份組會擷取根據 hello 下列參數：

* **時間範圍**– hello hello 備份集建立時的日期和時間範圍。
* **裝置**– hello 裝置的 hello 當初建立備份組。
* **備份原則**或**磁碟區**– hello 備份原則或與此備份組相關聯的磁碟區。

hello 篩選的備份組會再製成資料表根據 hello 下列屬性：

* **名稱**– hello hello 備份原則或 hello 備份組相關聯的磁碟區的名稱。
* **類型** - 備份組可以是本機快照集或雲端快照集。 本機快照是儲存在本機 hello 裝置上所有磁碟區資料的備份，而雲端快照是指位於 hello 雲端中的磁碟區 toohello 資料備份。 本機快照可提供更快速的存取，而雲端快照是選擇來進行資料復原。
* **大小**– hello hello 備份組的實際大小。
* **在建立**– hello 日期和建立 hello 備份時的時間。 
* **磁碟區**-hello 與 hello 備份組相關聯的磁碟區數目。
* **起始**– hello 備份可以自動根據 tooa 排程起始或由使用者手動。 （您可以使用備份原則 tooschedule 備份。 或者，您可以使用 hello**取得備份**選項 tootake 的互動式或隨選備份。)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>如何 toorestore 您的 StorSimple 磁碟區從備份

您可以使用 hello**備份類別目錄**刀鋒視窗 toorestore 您的 StorSimple 磁碟區，從特定的備份。 請記住，不過，還原磁碟區將會還原 hello hello 備份時的磁碟區 toohello 狀態。 已加入之後 hello 備份作業將會遺失任何資料。

> [!WARNING]
> 從備份還原，將會取代 hello hello 備份中的現有磁碟區。 這也可能造成 hello hello 備份後寫入任何資料遺失。


### <a name="toorestore-your-volume"></a>toorestore 您的磁碟區
1. 在 tooyour StorSimple 裝置管理員服務的 **備份類別目錄**。

2. 選取備份組，如下所示：
   
   1. 指定 hello 時間範圍。
   2. 選取 hello 適當的裝置。
   3. 在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。
   4. 按一下**套用**tooexecute 此查詢。

    hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。
   
    ![備份組清單](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. 展開 hello 備份組 tooview hello 相關聯的磁碟區。 這些磁碟區必須採取 hello 主機和裝置上離線再進行還原。 存取 hello 磁碟區上 hello**磁碟區**您的裝置，然後遵循 hello 刀鋒視窗中的步驟[使磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)tootake 離線。
   
   > [!IMPORTANT]
   > 請確定您已經執行 hello 磁碟區離線 hello 主機上的第一次之後您才能 hello 裝置上的 hello 磁碟區離線。 如果您不會在 hello 主機上取得 hello 磁碟區離線，有可能導致 toodata 損毀。
   
4. 瀏覽後 toohello**備份類別目錄**索引標籤並選取備份組。 以滑鼠右鍵按一下，然後從 hello 內容功能表中，選取**還原**。

    ![備份組清單](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. 系統將提示您進行確認。 檢閱 hello 還原的詳細資訊，，然後選取 hello 確認核取方塊。
   
    ![確認電子郵件](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  按一下 [還原]。 這會起始的還原作業，您可以藉由存取 hello 檢視**作業**頁面。

    ![確認電子郵件](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Hello 還原完成後，請確認您的磁碟區 hello 內容會取代從 hello 備份的磁碟區。


## <a name="if-hello-restore-fails"></a>如果 hello 還原失敗

如果 hello 還原作業將會失敗，因為任何原因，您會收到警示。 如果發生這種情況，hello 備份的重新整理 hello 備份清單 tooverify 為仍然有效。 如果 hello 備份有效，且您從 hello 雲端還原，然後連線問題可能導致 hello 問題。

toocomplete hello 還原作業，hello 主機上讓 hello 磁碟區離線，然後重試 hello 還原作業。 請注意 hello 期間所執行的任何修改 toohello 磁碟區資料還原程序將會遺失。

## <a name="next-steps"></a>後續步驟
* 了解如何太[管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

