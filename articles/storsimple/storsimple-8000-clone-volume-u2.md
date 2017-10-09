---
title: "aaaClone StorSimple 8000 系列上的磁碟區 |Microsoft 文件"
description: "描述 hello 複製不同類型和使用方式，並說明如何使用個別的磁碟區的備份組 tooclone StorSimple 8000 系列裝置上。"
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>在 Azure 入口網站 tooclone 磁碟區中使用 hello StorSimple 裝置管理員服務

## <a name="overview"></a>概觀

這個教學課程描述如何使用透過 hello 個別磁碟區的備份組 tooclone**備份類別目錄**刀鋒視窗。 它也會說明 hello 差異*暫時性*和*永久*複製。 本教學課程中的 hello 指導方針適用於 tooall hello StorSimple 8000 系列裝置執行 Update 3 或更新版本。

hello StorSimple 裝置管理員服務**備份類別目錄**刀鋒視窗會顯示所有 hello 的備份組時手動或自動備份所建立的。 然後，您可以在備份組 tooclone 選取磁碟區。

 ![備份組清單](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>複製磁碟區的考量

請考慮 hello 的磁碟區複製時，下列資訊。

- 複本的行為在 hello 相同與一般磁碟區的方式。 可以在磁碟區的任何作業是可用於 hello 複製。

- 複製的磁碟區上會自動停用監視和預設備份。 您需要的任何備份 tooconfigure 複製的磁碟區。

- 固定在本機的磁碟區會複製為分層磁碟區。 如果您需要 hello 固定在本機複製的磁碟區 toobe，您可以在 hello 複製作業成功完成之後，轉換 hello 複製 tooa 固定在本機磁碟區。 資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。

- 如果您嘗試複製的磁碟區，從階層式 toolocally 釘選之後立即複製 （當它仍然是暫時性複本） 的 tooconvert，hello 轉換會失敗並 hello 下列錯誤訊息：

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    只有當您正在複製 tooa 不同裝置上，會收到這個錯誤。 您可以成功地轉換 hello 磁碟區 toolocally 釘選，如果您先轉換 hello 暫時性複本 tooa 永久性複本。 雲端快照的 hello 暫時性複本 tooconvert 它 tooa 永久性複本。

## <a name="create-a-clone-of-a-volume"></a>建立磁碟區複製

您可以建立複本在 hello 相同裝置、 另一個裝置或甚至雲端應用裝置，使用本機或雲端快照集。

下列的 hello 程序描述如何 toocreate hello 從複本備份類別目錄。  替代方法 tooinitiate 複製太 toogo**磁碟區**、 選取的磁碟區，然後 tooinvoke hello 操作功能表上按一下滑鼠右鍵並選取**複製**。

執行 hello hello 備份類別目錄中的下列步驟 toocreate 您的磁碟區的複本。

#### <a name="tooclone-a-volume"></a>tooclone 磁碟區

1. 在 tooyour StorSimple 裝置管理員服務的 **備份類別目錄**。

2. 選取備份組，如下所示：
   
   1. 選取 hello 適當的裝置。
   2. 在 hello 下拉式清單中，選擇您想 tooselect hello hello 備份的磁碟區或備份原則。
   3. 指定 hello 時間範圍。
   4. 按一下**套用**tooexecute 此查詢。

    hello 與 hello 選取磁碟區或備份原則相關聯的備份清單應會顯示 hello 的備份組。
   
    ![備份組清單](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. 展開 hello 備份組 tooview hello 相關聯的磁碟區。 這些磁碟區必須採取 hello 主機和裝置上離線再進行還原。 存取 hello 磁碟區上 hello**磁碟區**您的裝置，然後遵循 hello 刀鋒視窗中的步驟[使磁碟區離線](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline)tootake 離線。
   
   > [!IMPORTANT]
   > 請確定您已經執行 hello 磁碟區離線 hello 主機上的第一次之後您才能 hello 裝置上的 hello 磁碟區離線。 如果您不會在 hello 主機上取得 hello 磁碟區離線，有可能導致 toodata 損毀。
   
4. 瀏覽後 toohello**備份類別目錄**和備份組中選取的磁碟區。 以滑鼠右鍵按一下，然後從 hello 內容功能表中，選取**複製**。

   ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. 在 hello**複製**刀鋒視窗中，執行下列步驟 hello:
   
    1. 識別目標裝置。 這是指將建立 hello 複製 hello 位置。 您可以選擇 hello 相同的裝置，或指定另一個裝置。

      > [!NOTE]
      > 請確定所需的 hello 複製 hello 容量低於 hello 目標裝置上可用的 hello 容量。
       
    2. 為複製指定唯一的磁碟區名稱。 hello 名稱必須包含 3 到 127 個字元。
      
        > [!NOTE]
        > hello**複製磁碟區做為**欄位就是**分層**即使您正在複製本機固定磁碟區。 您無法變更此設定。不過，如果您需要 hello 固定在本機以及複製的磁碟區 toobe，您可以先轉換 hello 複製 tooa 固定在本機磁碟區之後您已成功建立 hello 複製。 資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-8000-manage-volumes-u2.md#change-the-volume-type)。
          
    3. 在下**連線主機**，指定 hello 複製存取控制記錄 (ACR)。 您可以新增 ACR，或從 hello 現有清單中選擇。 hello ACR 會決定可存取此複本的主機。
      
        ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. 按一下**複製**toocomplete hello 作業。

4. 複製工作已起始，而且當 hello 複製建立成功時，會收到通知。 按一下 hello 工作通知或太到**作業**刀鋒視窗 toomonitor hello 複製工作。

    ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Hello 複製工作完畢之後，移 tooyour 裝置，然後按一下**磁碟區**。 在 [hello] 清單中的磁碟區，您應該會看到剛建立 hello 中相同的 hello 複製 hello 來源磁碟區的磁碟區容器。

    ![備份組清單](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

以這種方式建立的複製就是暫時性複製。 如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。


## <a name="transient-vs-permanent-clones"></a>暫時性與永久複製
只有當您複製 tooanother 裝置時，會建立暫時性的複製品。 您可以複製 hello StorSimple 裝置管理員所管理的備份組的 tooa 不同裝置中的特定磁碟區。 hello 暫時性複本 hello 原始磁碟區中有參考 toohello 資料，並使用該資料 tooread 和寫入本機 hello 目標裝置上。

您製作暫時性複本的雲端快照後，複製 hello 結果是*永久*複製。 在此過程中，一份 hello 資料建立 hello 雲端上 hello 時間 toocopy 這項資料由 hello 資料大小的 hello 和 hello Azure 延遲 （這是 Azure-Azure 複本）。 此程序可能需要天 tooweeks。 hello 暫時性複本會變成永久性複本，而沒有任何參考 toohello 原始磁碟區的資料，從已再製。

## <a name="scenarios-for-transient-and-permanent-clones"></a>暫時性複製與永久複製的案例
hello 下列各節將描述範例可以在其中使用暫時性和永久性複本的情況。

### <a name="item-level-recovery-with-a-transient-clone"></a>使用暫時性複製復原項目層級
您需要 toorecover 一個年度舊 Microsoft PowerPoint 簡報檔案。 IT 系統管理員識別 hello 這段時間，從特定的備份，然後篩選 hello 磁碟區。 hello 系統管理員，然後複製 hello 磁碟區、 找出您要尋找的 hello 檔案並提供它 tooyou。 在此案例中，使用的是暫時性複製。

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>在 hello 與永久性複本的實際執行環境中測試
您需要 tooverify hello 實際執行環境中測試錯誤。 您建立 hello 實際執行環境中的 hello 磁碟區的複本，然後再採取此複製 toocreate 獨立複製的磁碟區的雲端快照。 在此案例中，使用的是永久複製。

## <a name="next-steps"></a>後續步驟
* 了解如何太[StorSimple 磁碟區從備份組還原](storsimple-8000-restore-from-backup-set-u2.md)。
* 了解如何太[使用 hello StorSimple 裝置管理員服務 tooadminister StorSimple 裝置](storsimple-8000-manager-service-administration.md)。

