---
title: "aaaStorSimple Snapshot Manager 備份類別目錄 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooview 和管理 hello 備份類別目錄。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>使用 StorSimple Snapshot Manager toomanage hello 備份類別目錄

## <a name="overview"></a>概觀
hello 主要函式的 StorSimple Snapshot Manager 是的 tooallow 您 toocreate 應用程式一致備份複本的快照集的 hello 形式的 StorSimple 磁碟區。 快照集會列在稱為 *備份目錄*的 XML 檔案中。 hello 備份類別目錄會組織依磁碟區群組及本機快照或雲端快照的快照集。

這個教學課程描述如何使用 hello**備份類別目錄**節點 toocomplete hello 下列工作：

* 還原磁碟區
* 複製磁碟區或磁碟區群組
* 刪除備份
* 復原檔案
* 還原 hello Storsimple Snapshot Manager 資料庫

您可以檢視 hello 備份類別目錄的展開 hello**備份類別目錄**節點 hello**範圍**窗格中，然後再展開 hello 磁碟區群組。

* 如果您按一下 hello 磁碟區群組名稱，hello**結果** 窗格會顯示 hello 本機快照及雲端快照可用於 hello 磁碟區群組數目。 
* 如果您按一下**本機快照**或**雲端快照**，hello**結果** 窗格會顯示下列每個備份快照的相關資訊的 hello (根據您**檢視**設定):
  
  * **名稱**– hello 時間 hello 快照。
  * **類型** – 這是本機快照集或雲端快照集。
  * **擁有者**– hello 內容擁有者。 
  * **可用**– 是否 hello 快照集是目前可用。 **True**表示該 hello 快照集為可用，且可加以還原;**False**指出該 hello 快照集已無法再使用。 
  * **匯入**– 是否已匯入 hello 備份。 **True**指出 hello StorSimple 裝置管理員在 hello 時間 hello 裝置上的服務未設定 StorSimple Snapshot Manager 中; 從匯入該 hello 備份**False**表示它未匯入，但 StorSimple Snapshot Manager 所建立。 （您可以輕鬆地識別匯入的磁碟區群組因為可識別 hello 裝置 hello 磁碟區群組匯入的新增後置字元。）
    
    ![備份類別目錄](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* 如果您展開**本機快照**或**雲端快照**，然後按一下個別快照名稱，hello**結果** 窗格會顯示下列資訊 hello hello您選取的快照集：
  
  * **名稱**– hello 根據磁碟機代號的磁碟區。 
  * **本機名稱**– hello hello 磁碟機 （如果有的話） 的本機名稱。 
  * **裝置**– hello hello 裝置的 hello 所在磁碟區的名稱。 
  * **可用**– 是否 hello 快照集是目前可用。 **True**表示該 hello 快照集為可用，且可加以還原;**False**指出該 hello 快照集已無法再使用。 

## <a name="restore-a-volume"></a>還原磁碟區
使用下列程序 toorestore 磁碟區從備份中的 hello。

#### <a name="prerequisites"></a>必要條件
如果您尚未這樣做，請建立磁碟區和磁碟區群組，然後再刪除 hello 磁碟區。 根據預設，StorSimple Snapshot Manager 備份磁碟區之前允許它 toobe 刪除。 如果不小心刪除 hello 磁碟區，或需要復原，因為任何原因 toobe hello 資料，這樣的預防措施可以防止資料遺失。 

StorSimple Snapshot Manager 顯示 hello 下會在建立 hello 預防備份時的訊息。

![自動快照訊息](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> 您無法刪除磁碟區，因為它是磁碟區群組的一部分的。 hello 刪除選項無法使用。 <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore 磁碟區
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。 
2. 在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**] 節點，展開 [磁碟區群組，然後按一下**本機快照**或**雲端快照**. 備份快照清單會出現在 hello**結果**窗格。
3. Toorestore、 按一下滑鼠右鍵，然後再按一下您要尋找 hello 備份**還原**。
   
    ![還原備份目錄](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. 在 hello 確認頁面上，檢閱 hello 的詳細資訊，請輸入**確認**，然後按一下**確定**。 StorSimple Snapshot Manager 會使用 hello 備份 toorestore hello 磁碟區。
   
    ![還原確認訊息](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. 當它執行時，您可以監視 hello 還原動作。 在 [hello**範圍**] 窗格中，展開 hello**作業**節點，然後再按一下**執行**。 hello 工作詳細資料會出現在 hello**結果**窗格。 Hello 工作詳細資料 hello 還原作業完成時，會傳送的 toohello**過去 24 小時**清單。

## <a name="clone-a-volume-or-volume-group"></a>複製磁碟區或磁碟區群組
使用下列程序 toocreate 磁碟區或磁碟區群組的複本 （副本） hello。

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone 磁碟區或磁碟區群組
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**] 節點，展開 [磁碟區群組，然後按一下**雲端快照**。 備份清單會出現在 hello**結果**窗格。
3. 尋找 hello 磁碟區或磁碟區群組，您想 tooclone、 以滑鼠右鍵按一下 hello 磁碟區或磁碟區群組名稱，然後按一下 **複製**。 hello**複製雲端快照** 對話方塊隨即出現。
   
    ![複製雲端快照集](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. 完整的 hello**複製雲端快照**對話方塊中，如下所示： 
   
   1. 在 [hello**名稱**] 文字方塊中，輸入的名稱 hello 複製磁碟區。 這個名稱會出現在 hello**磁碟區**節點。 
   2. （選擇性） 選取**磁碟機**，然後從 hello 下拉式清單中選取磁碟機代號。
   3. （選擇性） 選取**資料夾 (NTFS)**，並輸入資料夾路徑，或按一下 瀏覽並選取 hello 資料夾位置。 
   4. 按一下 [建立] 。
5. Hello 複製程序完成時，您必須先初始化 hello 複製磁碟區。 啟動伺服器管理員，然後啟動磁碟管理。 如需詳細指示，請參閱 [掛接磁碟區](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)。 在初始化之後，將列 hello 磁碟區之下 hello**磁碟區**hello 節點**範圍**窗格。 如果看不到 hello 磁碟區列出，請重新整理的磁碟區的 hello 清單 (以滑鼠右鍵按一下 hello**磁碟區**節點，然後再按一下**重新整理**)。

## <a name="delete-a-backup"></a>刪除備份
使用 hello hello 備份類別目錄中的下列程序 toodelete 快照集。 

> [!NOTE]
> 刪除快照會刪除 hello 備份 hello 快照集相關聯的資料。 不過，hello 的從 hello 雲端清除資料的程序可能需要一些時間。<br>


#### <a name="toodelete-a-backup"></a>toodelete 備份
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**] 節點，展開 [磁碟區群組，然後按一下**本機快照**或**雲端快照**. 快照清單會出現在 hello**結果**窗格。
3. 以滑鼠右鍵按一下您想 toodelete，然後再按一下 hello 快照**刪除**。
4. Hello 確認訊息出現時，按一下**確定**。

## <a name="recover-a-file"></a>復原檔案
如果不小心刪除檔案時從磁碟區，您可以藉由擷取預先日期 hello 刪除、 使用 hello 快照 toocreate 的快照集的 hello 大量複製復原 hello 檔案，然後複製從 hello 檔案 hello 複製的磁碟區 toohello 原始磁碟區。

#### <a name="prerequisites"></a>必要條件
在開始之前，請確定您擁有 hello 磁碟區群組的目前備份。 然後，刪除儲存在其中一個該磁碟區群組中的 hello 磁碟區上的檔案。 最後，使用您的備份中的下列步驟 toorestore hello 刪除檔案的 hello。 

#### <a name="toorecover-a-deleted-file"></a>toorecover 已刪除的檔案
1. 按一下桌面上的 hello StorSimple Snapshot Manager 圖示。 hello StorSimple Snapshot Manager 主控台 視窗隨即出現。 
2. 在 [hello**範圍**] 窗格中，展開 hello**備份類別目錄**節點，然後瀏覽 tooa 快照集，其中包含 hello 刪除檔案。 一般而言，您應該選取 hello 刪除之前建立的快照集。
3. 您想 tooclone，按一下滑鼠右鍵，然後按一下 尋找 hello 磁碟區**複製**。 hello**複製雲端快照** 對話方塊隨即出現。
   
    ![複製雲端快照集](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. 完整的 hello**複製雲端快照**對話方塊中，如下所示： 
   
   1. 在 [hello**名稱**] 文字方塊中，輸入的名稱 hello 複製磁碟區。 這個名稱會出現在 hello**磁碟區**節點。 
   2. （選擇性）選取**磁碟機**，然後從 hello 下拉式清單中選取磁碟機代號。 
   3. （選擇性）選取**資料夾 (NTFS)**，然後輸入資料夾路徑，或按一下**瀏覽**選取 hello 資料夾的位置。 
   4. 按一下 [建立] 。 
5. Hello 複製程序完成時，您必須先初始化 hello 複製磁碟區。 啟動伺服器管理員，然後啟動磁碟管理。 如需詳細指示，請參閱 [掛接磁碟區](storsimple-snapshot-manager-manage-volumes.md#mount-volumes)。 在初始化之後，將列 hello 磁碟區之下 hello**磁碟區**hello 節點**範圍**窗格。 
   
    如果看不到 hello 磁碟區列出，請重新整理的磁碟區的 hello 清單 (以滑鼠右鍵按一下 hello**磁碟區**節點，然後再按一下**重新整理**)。
6. 開啟 hello NTFS 資料夾包含 hello 複製磁碟區，展開 hello**磁碟區**節點，然後再開啟 hello 複製磁碟區。 尋找您想 toorecover，並將它複製 toohello 主要磁碟區的 hello 檔案。
7. 還原 hello 檔案之後，您可以刪除 hello 包含 hello 複製磁碟區的 NTFS 資料夾。

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>還原 hello StorSimple Snapshot Manager 資料庫
您應該定期備份 hello hello 主機電腦上的 StorSimple Snapshot Manager 資料庫。 如果發生損毀或因任何原因失敗 hello 主機電腦，然後可以將它從 hello 備份中還原。 建立 hello 資料庫備份是手動程序。

#### <a name="tooback-up-and-restore-hello-database"></a>向上 tooback 和還原 hello 資料庫
1. 停止 Microsoft StorSimple 管理服務的 hello:
   
   1. 啟動伺服器管理員。
   2. Hello 伺服器管理員儀表板上，在 hello**工具**功能表上，選取**服務**。
   3. 在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。
   4. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。
2. Hello 主機電腦上，瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。 
   
   > [!NOTE]
   > ProgramData 是隱藏的資料夾。
   > 
   > 
3. 尋找 hello 類別目錄 XML 檔案，複製 hello 檔案，並存放區 hello 複製在安全的位置或 hello 雲端中。 如果 hello 主機失敗，您可以使用這個備份檔案 toohelp 復原 hello 備份原則建立 StorSimple Snapshot Manager 中。
   
    ![Azure StorSimple 備份目錄檔案](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. 重新啟動 Microsoft StorSimple 管理服務的 hello: 
   
   1. Hello 伺服器管理員儀表板上，在 hello**工具**功能表上，選取**服務**。
   2. 在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。
   3. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。
5. Hello 主機電腦上，瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。 
6. 刪除 hello 類別目錄 XML 檔案，然後 hello 您所建立的備份版本取代它。 
7. 按一下桌面 StorSimple Snapshot Manager 圖示 toostart hello StorSimple Snapshot Manager。 

## <a name="next-steps"></a>後續步驟
* 深入了解[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 深入了解 [StorSimple Snapshot Manager 工作和工作流程](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows)。

