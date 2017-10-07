---
title: "aaaClone StorSimple 8000 系列的磁碟區 |Microsoft 文件"
description: "描述 hello 複製不同類型和當 toouse 它們，並說明如何使用備份組 tooclone 個別磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>使用 hello StorSimple Manager 服務 tooclone (Update 2) 的磁碟區
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>概觀
StorSimple Manager 服務的 hello**備份類別目錄**頁面會顯示所有 hello 的備份組時手動或自動備份所建立的。 您可以使用此頁面 toolist hello 的所有備份的備份原則或磁碟區，選取或刪除的備份，或都使用備份 toorestore 或複製磁碟區。

![備份類別目錄頁面](./media/storsimple-clone-volume-u2/backupCatalog.png)  

本教學課程說明如何使用備份組 tooclone 個別磁碟區。 它也會說明 hello 差異*暫時性*和*永久*複製。

> [!NOTE]
> 固定在本機的磁碟區將會複製為分層磁碟區。 如果您需要 hello 固定在本機複製的磁碟區 toobe，您可以在 hello 複製作業成功完成之後，轉換 hello 複製 tooa 固定在本機磁碟區。 資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。
> 
> 如果您嘗試複製的磁碟區，從階層式 toolocally 釘選之後立即複製 （當它仍然是暫時性複本） 的 tooconvert，hello 轉換會失敗並 hello 下列錯誤訊息：
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> 只有當您正在複製 tooa 不同裝置上，會收到這個錯誤。 您可以成功地轉換 hello 磁碟區 toolocally 釘選，如果您先轉換 hello 暫時性複本 tooa 永久性複本。 tooconvert hello 暫時性複本 tooa 永久複製，建立它的雲端快照。
> 
> 

## <a name="create-a-clone-of-a-volume"></a>建立磁碟區複製
您可以建立複本在 hello 相同裝置、 另一個裝置或甚至虛擬機器使用本機或雲端快照集。

#### <a name="tooclone-a-volume"></a>tooclone 磁碟區
1. 在 hello StorSimple Manager 服務頁面上，按一下 hello**備份類別目錄**索引標籤並選取備份組。
2. 展開 hello 備份組 tooview hello 相關聯的磁碟區。 按一下並選取從 hello 備份集的磁碟區。
   
     ![複製磁碟區](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. 按一下**複製**toobegin hello 選取磁碟區複製。
4. 在 hello 複製磁碟區精靈下**指定名稱和位置**:
   
   1. 識別目標裝置。 這是指將建立 hello 複製 hello 位置。 您可以選擇 hello 相同的裝置，或指定另一個裝置。 如果您選擇其他雲端服務提供者相關聯的磁碟區 (不 Azure) hello 下拉式清單的 hello 目標裝置只會顯示實體裝置。 您無法在虛擬裝置上複製與其他雲端服務提供者相關聯的磁碟區。
      
      > [!NOTE]
      > 請確定所需的 hello 複製 hello 容量低於 hello 目標裝置上可用的 hello 容量。
      > 
      > 
   2. 為複製指定唯一的磁碟區名稱。 hello 名稱必須包含 3 到 127 個字元。 
      
      > [!NOTE]
      > hello**複製磁碟區做為**欄位就是**分層**即使您正在複製本機固定磁碟區。 您無法變更此設定。不過，如果您需要 hello 固定在本機以及複製的磁碟區 toobe，您可以先轉換 hello 複製 tooa 固定在本機磁碟區之後您已成功建立 hello 複製。 資訊轉換分層磁碟區 tooa 本機固定磁碟區，請移過[變更 hello 磁碟區類型](storsimple-manage-volumes-u2.md#change-the-volume-type)。
      > 
      > 
      
        ![複製精靈 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. 按一下 [hello] 箭號圖示 ![arrow-icon](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello 下一個頁面。
5. 在 [指定可以使用此磁碟區的主機] 下：
   
   1. 指定 hello 複製存取控制記錄 (ACR)。 您可以新增 ACR，或從 hello 現有清單中選擇。
      
        ![複製精靈 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. 按一下 [hello] 核取圖示 ![核取圖示](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)toocomplete hello 作業。
6. 會起始複製工作，且當 hello 複製建立成功時將會通知您。 按一下**檢視工作**toomonitor hello 複製工作上 hello**作業**頁面。 您會看見 hello hello 複製工作完畢時，下列訊息：
   
    ![複製訊息](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. 複製工作已完成之後 hello:
   
   1. 移 toohello**裝置** 頁面上，並選取 hello**磁碟區容器** 索引標籤。 
   2. 選取 hello 與您用於複製的 hello 來源磁碟區相關聯的磁碟區容器。 在 hello 清單中的磁碟區，您應該會看到剛才建立的 hello 複製。

> [!NOTE]
> 複製的磁碟區上會自動停用監視和預設備份。
> 
> 

以這種方式建立的複製就是暫時性複製。 如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。

此複製現在是一般的磁碟區，並可以在磁碟區任何作業都可用於 hello 複製。 您需要 tooconfigure 此磁碟區進行任何備份。

## <a name="transient-vs-permanent-clones"></a>暫時性與永久複製
只有當您正在複製 tooa 不同的裝置時，會建立暫時性的複製品。 您可以複製 hello StorSimple Manager 所管理的備份組的 tooa 不同裝置中的特定磁碟區。 hello 暫時性複本會 hello 原始磁碟區中有參考 toohello 資料和將使用該資料 tooread 並直接在本機寫入 hello 目標裝置上。 

您製作暫時性複本的雲端快照後，將會複製 hello 結果*永久*複製。 在此過程中，一份 hello 資料建立 hello 雲端上 hello 時間 toocopy 這項資料由 hello 資料大小的 hello 和 hello Azure 延遲 （這是 Azure-Azure 複本）。 此程序可能需要天 tooweeks。 hello 暫時性複本會變成永久性複本這種方式，而沒有任何參考 toohello 原始磁碟區的資料，從已再製。 

## <a name="scenarios-for-transient-and-permanent-clones"></a>暫時性複製與永久複製的案例
hello 下列各節將描述範例可以在其中使用暫時性和永久性複本的情況。

### <a name="item-level-recovery-with-a-transient-clone"></a>使用暫時性複製復原項目層級
您需要 toorecover 一個年度舊 Microsoft PowerPoint 簡報檔案。 IT 系統管理員識別 hello 從該時間範圍內，特定的備份，然後篩選 hello 磁碟區。 hello 系統管理員，然後複製 hello 磁碟區、 找出您要尋找的 hello 檔案並提供它 tooyou。 在此案例中，使用的是暫時性複製。 

![提供的影片](./media/storsimple-clone-volume-u2/Video_icon.png) **提供的影片**

toowatch 的影片示範如何使用 hello 複製和還原功能在 StorSimple toorecover 刪除檔案中，按一下[這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>在 hello 與永久性複本的實際執行環境中測試
您需要 tooverify hello 實際執行環境中測試錯誤。 您建立 hello 實際執行環境中的 hello 磁碟區的複本，然後再採取此複製 toocreate 獨立複製的磁碟區的雲端快照。 在此案例中，使用的是永久複製。  

## <a name="next-steps"></a>後續步驟
* 了解如何太[StorSimple 磁碟區從備份組還原](storsimple-restore-from-backup-set-u2.md)。
* 了解如何太[使用 hello StorSimple Manager 服務 tooadminister StorSimple 裝置](storsimple-manager-service-administration.md)。

