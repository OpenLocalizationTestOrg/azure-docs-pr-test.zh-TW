---
title: "aaaStorSimple Snapshot Manager 磁碟區群組 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 toocreate 和管理磁碟區群組。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>使用 StorSimple Snapshot Manager toocreate 及管理磁碟區群組
## <a name="overview"></a>概觀
您可以使用 hello**磁碟區群組**節點上 hello**範圍**窗格 tooassign 磁碟區 toovolume 群組，檢視資訊的磁碟區群組，排程備份，並編輯磁碟區群組。

磁碟區群組是使用相關的磁碟區 tooensure 備份是應用程式一致的集區。 如需詳細資訊，請參閱[磁碟區和磁碟區群組](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups)，以及[與 Windows 磁碟區陰影複製服務整合](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)。

> [!IMPORTANT]
> * 磁碟區群組中的所有磁碟區必須來自單一雲端服務提供者。
> * 當您設定磁碟區群組時，請勿混用叢集共用磁碟區 (Csv) 和非 Csv hello 中相同的磁碟區群組。 StorSimple Snapshot Manager 不支援混用 Csv 和非 Csv 中 hello 相同的快照集。

![磁碟區群組節點](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**圖 1：StorSimple Snapshot Manager 磁碟區群組節點** 

本教學課程說明如何使用 StorSimple Snapshot Manager：

* 檢視磁碟區群組的相關資訊
* 建立磁碟區群組
* 備份磁碟區群組
* 編輯磁碟區群組
* 刪除磁碟區群組

所有這些動作也會提供在 hello**動作**窗格。

## <a name="view-volume-groups"></a>檢視磁碟區群組
如果您按一下 hello**磁碟區群組**節點、 hello**結果** 窗格會顯示 hello 下列每個磁碟區群組的相關資訊，請根據 hello 資料行的選項。 (hello hello 中的資料行**結果**窗格可加以設定。 以滑鼠右鍵按一下 hello**磁碟區**節點中，選取**檢視**，然後選取**新增/移除欄位**。)

| 結果資料行 | 說明 |
|:--- |:--- |
| 名稱 |hello**名稱**資料行包含 hello hello 磁碟區群組名稱。 |
| 應用程式 |hello**應用程式**欄顯示 hello 號碼目前已安裝的 VSS 寫入器和上執行 hello Windows 主機。 |
| 已選取 |hello**選取**資料行會顯示 hello 磁碟區群組中所包含的磁碟區的 hello 數目。 零 (0) 表示沒有任何應用程式都與 hello hello 磁碟區群組中的磁碟區。 |
| 已匯入 |hello**已匯入**資料行會顯示 hello 匯入的磁碟區數目。 當設定太**True**，此資料行表示磁碟區群組從 hello Azure 入口網站匯入，而且未建立 StorSimple Snapshot Manager 中。 |

> [!NOTE]
> StorSimple Snapshot Manager 磁碟區群組也會顯示在 hello**備份原則**hello Azure 入口網站中的索引標籤。
> 
> 

## <a name="create-a-volume-group"></a>建立磁碟區群組
使用下列程序 toocreate 磁碟區群組的 hello。

#### <a name="toocreate-a-volume-group"></a>toocreate 磁碟區群組
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**磁碟區群組**，然後按一下**建立磁碟區群組**。
   
    ![建立磁碟區群組](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    hello**建立磁碟區群組** 對話方塊隨即出現。
   
    ![建立磁碟區群組對話方塊](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. 輸入下列資訊的 hello:
   
   1. 在 hello**名稱**方塊中，輸入 hello 新磁碟區群組的唯一名稱。
   2. 在 hello**應用程式**方塊中，選取與 hello 磁碟區，您會將加入 toohello 磁碟區群組相關聯的應用程式。
      
       hello**應用程式** 方塊中列出的那些應用程式使用 StorSimple 磁碟區且具有 VSS 寫入器啟用它們。 VSS 寫入器已啟用，只有在所有 hello 磁碟區 hello 寫入器注意的是 StorSimple 磁碟區。 如果 hello 應用程式 方塊是空的然後才會不安裝任何應用程式，使用 Azure StorSimple 磁碟區，並支援 VSS 寫入器。 (目前，Azure StorSimple 支援 Microsoft Exchange 和 SQL Server)。如需 VSS 寫入器的詳細資訊，請參閱[與 Windows 磁碟區陰影複製服務整合](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service)。
      
       如果選取應用程式，則會自動選取所有與其相關聯的磁碟區。 相反地，如果您選取特定的應用程式相關聯的磁碟區，hello 應用程式中自動選取 hello**應用程式**方塊。 
   3. 在 hello**磁碟區**方塊中，選取 StorSimple 磁碟區 tooadd toohello 磁碟區群組。 
      
      * 您可以包含具有單一或多個磁碟分割的磁碟區。 (多個磁碟分割磁碟區可以是具有多個磁碟分割的動態磁碟或基本磁碟)。包含多個磁碟分割的磁碟區會被視為單一單位。 因此，如果您將其中一個 hello 分割 tooa 磁碟區群組，所有的 hello 加入了其他資料分割會自動新增的 toothat 磁碟區群組在 hello 相同的時間。 您加入多個資料分割的磁碟區 tooa 磁碟區群組之後，hello 多個磁碟分割磁碟區會繼續 toobe 當做單一單位來處理。
      * 您可以建立空的磁碟區群組未指派任何磁碟區 toothem。 
      * 請勿混用叢集共用磁碟區 (Csv) 和非 Csv hello 中相同的磁碟區群組。 StorSimple Snapshot Manager 不支援混用 CSV 磁碟區和非 CSV 磁碟區中的 hello 相同的快照集。
4. 按一下**確定**toosave hello 磁碟區群組。

## <a name="back-up-a-volume-group"></a>備份磁碟區群組
使用下列程序 tooback 磁碟區群組的 hello。

#### <a name="tooback-up-a-volume-group"></a>tooback 磁碟區群組
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，展開 hello**磁碟區群組** 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後**取得備份**。
   
    ![立即備份磁碟區群組](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. 在 hello**取得備份**對話方塊中，選取**本機快照**或**雲端快照**，然後按一下**建立**。
   
    ![取得備份對話方塊](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. hello 備份的 tooconfirm 正在執行中，展開 hello**作業**節點，然後再按一下**執行**。 應該會列出 hello 備份。
5. tooview hello 完成快照集，請展開 hello**備份類別目錄** 節點，展開 hello 磁碟區群組名稱，然後按一下**本機快照**或**雲端快照**。 如果它已順利完成，將會列出 hello 備份。

## <a name="edit-a-volume-group"></a>編輯磁碟區群組
使用下列程序 tooedit 磁碟區群組的 hello。

#### <a name="tooedit-a-volume-group"></a>tooedit 磁碟區群組
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，展開 hello**磁碟區群組** 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後**編輯**。
3. hello * * 建立磁碟區群組 * * 對話方塊隨即出現。 您可以變更 hello**名稱**，**應用程式**，和**磁碟區**項目。
4. 按一下**確定**toosave 您的變更。

## <a name="delete-a-volume-group"></a>刪除磁碟區群組
使用下列程序 toodelete 磁碟區群組的 hello。 

> [!WARNING]
> 這也會刪除所有與 hello 磁碟區群組相關聯的 hello 備份。
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete 磁碟區群組
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，展開 hello**磁碟區群組** 節點，以滑鼠右鍵按一下磁碟區群組名稱，然後**刪除**。
3. hello**刪除磁碟區群組** 對話方塊隨即出現。 型別**確認**在 hello 文字方塊中，然後按一下**確定**。
   
    從在 hello hello 清單消失 hello 刪除磁碟區群組**結果**窗格和與該磁碟區群組相關聯的所有備份都會從 hello 備份類別目錄刪除。

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 了解如何太[使用 StorSimple Snapshot Manager toocreate 及管理備份原則](storsimple-snapshot-manager-manage-backup-policies.md)。

