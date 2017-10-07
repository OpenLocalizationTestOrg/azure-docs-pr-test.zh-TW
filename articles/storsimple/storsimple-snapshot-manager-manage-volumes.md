---
title: "aaaStorSimple Snapshot Manager 和磁碟區 |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooview 和管理磁碟區和 tooconfigure 備份。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>使用 StorSimple Snapshot Manager tooview 及管理磁碟區
## <a name="overview"></a>概觀
您可以使用 hello StorSimple Snapshot Manager**磁碟區**節點 (在 hello**範圍**窗格) tooselect 磁碟區，並檢視其相關資訊。 hello 磁碟區會顯示為對應 toohello hello 主機所掛接的磁碟區的磁碟機。 hello**磁碟區**節點會顯示本機磁碟區和支援的 StorSimple，包括透過 iSCSI 及裝置 hello 使用探索到的磁碟區的磁碟區類型。 

如需有關支援的磁碟區的詳細資訊，請移至太[支援多個磁碟區類型](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types)。

![在 [結果] 窗格中的磁碟區清單](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

hello**磁碟區**節點也可讓您重新掃描或刪除磁碟區之後 StorSimple Snapshot Manager 探索它們。 

本教學課程說明如何掛載、初始化和格式化磁碟區，然後使用 StorSimple Snapshot Manager：

* 檢視磁碟區的相關資訊 
* 刪除磁碟區
* 重新掃描磁碟區 
* 設定基本磁碟區並將其備份
* 設定動態鏡像磁碟區並將其備份

> [!NOTE]
> 所有 hello**磁碟區**節點動作也會提供在 hello**動作**窗格。
> 
> 

## <a name="mount-volumes"></a>掛接磁碟區
使用 hello 下列程序 toomount 初始化及格式化 StorSimple 磁碟區。 此程序會使用磁碟管理 中的系統公用程式管理硬碟與 hello 對應的磁碟區或磁碟分割。 如需磁碟管理的詳細資訊，請移過[磁碟管理](https://technet.microsoft.com/library/cc770943.aspx)hello Microsoft TechNet 網站上。

#### <a name="toomount-volumes"></a>toomount 磁碟區
1. 在您的主機電腦上啟動 hello Microsoft iSCSI 啟動器。
2. 提供一個 hello 介面 IP 位址為 「 hello 目標入口網站或探索 IP 位址，然後再 toohello 裝置連線。 Hello 裝置連線之後，hello 磁碟區會存取 tooyour Windows 系統。 如需有關使用 hello Microsoft iSCSI 啟動器的詳細資訊，請進入 toohello > 一節 「 連接 tooan iSCSI 目標裝置 」[安裝和設定 Microsoft iSCSI 啟動器][1]。
3. 使用任何下列選項 toostart 磁碟管理的 hello:
   
   * 輸入 hello Diskmgmt.msc**執行**方塊。
   * 啟動 伺服器管理員中，展開 hello**儲存體**節點，然後再選取**磁碟管理**。
   * 啟動**系統管理工具**，依序展開 hello**電腦管理**節點，然後再選取**磁碟管理**。 
     
     > [!NOTE]
     > 您必須使用系統管理員權限 toorun 磁碟管理。
     > 
     > 
4. 線上採取 hello 的磁碟區：
   
   1. 在 [磁碟管理] 中，以滑鼠右鍵按一下任何標示為 [離線] 的磁碟區。
   2. 按一下 [重新啟動磁碟] 。 hello 磁碟應標示為**線上**hello 磁碟重新啟動之後。
5. 初始化 hello 的磁碟區：
   
   1. 以滑鼠右鍵按一下探索到的 hello 磁碟區。
   2. 在 hello 功能表中，選取 **初始化磁碟**。
   3. 在 hello**初始化磁碟**對話方塊中，您想 tooinitialize，然後再按一下選取的 hello 磁碟**確定**。
6. 格式化簡單磁碟區：
   
   1. 以滑鼠右鍵按一下您想 tooformat 磁碟區。
   2. 在 hello 功能表中，選取 **新增簡單磁碟區**。
   3. 使用 hello 新增簡單磁碟區精靈 tooformat hello 磁碟區：
      
      * 指定 hello 磁碟區大小。
      * 提供磁碟機代號。
      * 選取 hello NTFS 檔案系統。
      * 指定 64 KB 的配置單位大小。
      * 執行快速格式化。
7. 格式化多重磁碟分割磁碟區。 如需指示，請移 toohello 區段中，「 磁碟分割與磁碟區 」[實作磁碟管理](https://msdn.microsoft.com/library/dd163556.aspx)。

## <a name="view-information-about-your-volumes"></a>檢視您磁碟區的相關資訊
使用下列程序 tooview 資訊有關本機和 Azure StorSimple 磁碟區的 hello。

#### <a name="tooview-volume-information"></a>tooview 磁碟區資訊
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。 
2. 在 [hello**範圍**] 窗格中，按一下 hello**磁碟區**節點。 本機與掛接磁碟區，包括所有 Azure StorSimple 磁碟區，清單會出現在 hello**結果**窗格。 hello hello 中的資料行**結果**窗格可加以設定。 (以滑鼠右鍵按一下 hello**磁碟區**節點中，選取**檢視**，然後選取**新增/移除欄位**。)
   
    ![設定 hello 資料行](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | 結果資料行 | 說明 |
   |:--- |:--- |
   |  名稱 |hello**名稱**資料行包含 hello 磁碟機代號指派 tooeach 探索到的磁碟區。 |
   |  裝置 |hello**裝置**資料行包含 hello hello 裝置連線的 toohello 主機電腦的 IP 位址。 |
   |  裝置磁碟區名稱 |hello**裝置磁碟區名稱**資料行包含 hello 名稱 hello 裝置磁碟區 toowhich hello 選取磁碟區所屬。 這是定義在 hello 該特定磁碟區的 Azure 入口網站中的 hello 磁碟區名稱。 |
   |  存取路徑 |hello**存取路徑**資料行會顯示 hello 存取路徑 toohello 磁碟區。 這是 hello 存取磁碟機代號或掛接點的 hello 在磁碟區 hello 主機電腦上。 |

## <a name="delete-a-volume"></a>刪除磁碟區
使用下列程序 toodelete 磁碟區從 StorSimple Snapshot Manager hello。

> [!NOTE]
> 如果磁碟區是任何磁碟區群組的一部分，則無法刪除。 （hello 刪除選項不適用於磁碟區的磁碟區群組的成員。）您必須刪除 hello 整個磁碟區群組 toodelete hello 磁碟區。

#### <a name="toodelete-a-volume"></a>toodelete 磁碟區
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，按一下 hello**磁碟區**節點。 
3. 在 hello**結果**窗格中，以滑鼠右鍵按一下您想 toodelete 的 hello 磁碟區。
4. 在 [hello] 功能表上按一下**刪除**。 
   
    ![刪除磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. hello**刪除磁碟區** 對話方塊隨即出現。 型別**確認**在 hello 文字方塊中，然後按一下**確定**。
6. 根據預設，StorSimple Snapshot Manager 會先備份磁碟區，再將其刪除。 此預防措施可以保護您免於資料遺失如果 hello 刪除是無意。 StorSimple Snapshot Manager 顯示**自動快照**hello 磁碟區備份時的進度訊息。 
   
    ![自動快照訊息](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>重新掃描磁碟區
使用下列程序 toorescan hello 磁碟區連接的 tooStorSimple Snapshot Manager hello。

#### <a name="toorescan-hello-volumes"></a>toorescan hello 磁碟區
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**磁碟區**，然後按一下**重新掃描磁碟區**。
   
    ![重新掃描磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    此程序同步處理 hello 磁碟區清單與 StorSimple Snapshot Manager。 例如新的磁碟區或已刪除的磁碟區的任何變更將反映在 hello 結果中。

## <a name="configure-and-back-up-a-basic-volume"></a>設定和備份基本磁碟區
使用下列程序 tooconfigure 的基本磁碟區，備份的 hello 然後立即啟動備份，或建立排定的備份原則。

### <a name="prerequisites"></a>必要條件
開始之前：

* 請確定已正確設定 hello StorSimple 裝置與主機電腦。 如需詳細資訊，請移至太[部署在內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。
* 安裝和設定 StorSimple Snapshot Manager。 如需詳細資訊，請移至太[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>tooconfigure 的基本磁碟區備份
1. Hello StorSimple 裝置上建立基本磁碟區。
2. 掛接、 初始化及格式化 hello 磁碟區中所述[掛接磁碟區](#mount-volumes)。 
3. 按一下桌面上的 hello StorSimple Snapshot Manager 圖示。 hello StorSimple Snapshot Manager 視窗隨即出現。 
4. 在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**磁碟區**節點，然後再選取**重新掃描磁碟區**。 Hello 掃描完成時，磁碟區清單應該會出現在 hello**結果**窗格。 
5. 在 [hello**結果**] 窗格中，hello 磁碟區，以滑鼠右鍵按一下，然後選取**建立磁碟區群組**。 
   
    ![建立磁碟區群組](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. 在 hello**建立磁碟區群組**對話方塊中，輸入 hello 磁碟區群組的名稱，指定磁碟區 tooit，然後按一下**確定**。
7. 在 [hello**範圍**] 窗格中，展開 hello**磁碟區群組**節點。 hello 新磁碟區群組應該會出現在 hello**磁碟區群組**節點。 
8. 以滑鼠右鍵按一下 hello 磁碟區群組名稱。
   
   * 按一下 toostart 互動式 （隨） 備份工作，**取得備份**。 
   * tooschedule 的自動備份中，按一下**建立備份原則**。 在 hello**一般**頁面上，從 hello 清單中選取磁碟區群組。 在 hello**排程**頁面上，輸入 hello 排程詳細資料。 完成時，請按一下 [確定] 。 
9. hello 備份作業的 tooconfirm 已啟動，展開 [hello**作業**節點 hello**範圍**] 窗格中，然後按一下hello**執行**節點。 hello 清單目前執行的工作會出現在 hello**結果**窗格。 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>設定和備份動態鏡像磁碟區
完成下列步驟 tooconfigure 備份動態鏡像磁碟區的 hello:

* 步驟 1： 使用 磁碟管理 toocreate 動態鏡像磁碟區。 
* 步驟 2： 使用 StorSimple Snapshot Manager tooconfigure 備份。

### <a name="prerequisites"></a>必要條件
開始之前：

* 請確定已正確設定 hello StorSimple 裝置與主機電腦。 如需詳細資訊，請移至太[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。
* 安裝和設定 StorSimple Snapshot Manager。 如需詳細資訊，請移至太[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。
* Hello StorSimple 裝置上設定兩個磁碟區。 (在 hello 範例與 hello 可用的磁碟區為**磁碟 1**和**磁碟 2**。) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>步驟 1： 使用 磁碟管理 toocreate 動態鏡像磁碟區
磁碟管理 是管理硬碟與 hello 磁碟區或其所包含的資料分割的系統公用程式。 如需磁碟管理的詳細資訊，請移過[磁碟管理](https://technet.microsoft.com/library/cc770943.aspx)hello Microsoft TechNet 網站上。

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate 動態鏡像磁碟區
1. 使用任何下列選項 toostart 磁碟管理的 hello: 
   
   * 開啟 hello**執行**方塊中，輸入**Diskmgmt.msc**，然後按 Enter。
   * 啟動 伺服器管理員中，展開 hello**儲存體**節點，然後再選取**磁碟管理**。 
   * 啟動**系統管理工具**，依序展開 hello**電腦管理**節點，然後再選取**磁碟管理**。 
2. 請確定您有兩個可用的磁碟區 hello StorSimple 裝置上。 (在 hello 範例與 hello 可用的磁碟區為**磁碟 1**和**磁碟 2**。) 
3. 在 hello 磁碟管理 視窗，hello 右邊資料行中的 hello 下方窗格中，以滑鼠右鍵按一下**磁碟 1**選取**新增鏡像磁碟區**。 
   
    ![新鏡像磁碟區](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. 在 hello**新增鏡像磁碟區**精靈頁面上，按一下 **下一步**。
5. 在 hello**選取磁碟**頁面上，選取**磁碟 2**在 hello**選取** 窗格中，按一下**新增**，然後按一下**下一步**. 
6. 在 hello**指派磁碟機代號或路徑**頁面上，接受 hello 的預設值，然後按一下**下一步**。 
7. 在 hello**磁碟區格式化** 頁面的 hello**配置單位大小**方塊中，選取**64k**。 選取 hello**執行快速格式化**核取方塊，然後**下一步**。 
8. 在 hello**完成 hello 新增鏡像磁碟區**頁面上，檢閱您的設定，然後按一下**完成**。 
9. Hello 基本磁碟的 tooindicate 才會轉換的 tooa 動態磁碟會出現訊息。 按一下 [是] 。
   
    ![動態磁碟轉換訊息](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. 在磁碟管理中，確認磁碟區 1 與磁碟區 2 顯示為動態鏡像磁碟區。 (**動態**應該出現在 hello 狀態 資料行，而且 hello 容量列顏色應變成 toored，指出鏡像磁碟區。) 
    
    ![磁碟管理的鏡像動態磁碟](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>步驟 2： 使用 StorSimple Snapshot Manager tooconfigure 備份
使用下列程序 tooconfigure 動態鏡像磁碟區的 hello 然後立即啟動備份，或建立排定的備份原則。

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>動態鏡像磁碟區的 tooconfigure 備份
1. 按一下桌面上的 hello StorSimple Snapshot Manager 圖示。 hello StorSimple Snapshot Manager 視窗隨即出現。 
2. 在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**磁碟區**節點，然後選取**重新掃描磁碟區**。 Hello 掃描完成時，磁碟區清單應該會出現在 hello**結果**窗格。 hello 動態鏡像磁碟區會列示為單一磁碟區。 
3. 在 [hello**結果**] 窗格中，hello 動態的鏡像磁碟區上按一下滑鼠右鍵，然後按一下**建立磁碟區群組**。 
4. 在 hello**建立磁碟區群組**對話方塊中，輸入 hello 磁碟區群組的名稱，指派 hello 動態鏡像磁碟區 toothis 群組，然後按一下**確定**。 
5. 在 [hello**範圍**] 窗格中，展開 hello**磁碟區群組**節點。 hello 新磁碟區群組應該會出現在 hello**磁碟區群組**節點。 
6. 以滑鼠右鍵按一下 hello 磁碟區群組名稱。 
   
   * 按一下 toostart 互動式 （隨） 備份工作，**取得備份**。 
   * tooschedule 的自動備份中，按一下**建立備份原則**。 在 hello**一般**頁面上，選取 hello hello 清單中的磁碟區群組。 在 hello**排程**頁面上，輸入 hello 排程詳細資料。 完成時，請按一下 [確定] 。 
7. 當它執行時，您可以監視 hello 備份工作。 在 hello**範圍** 窗格中，展開 hello**作業**節點，然後再按一下**執行**，hello 工作詳細資料會出現在 hello**結果**窗格。 Hello 詳細資料 hello 備份工作完成時，會傳送的 toohello**過去 24**小時作業清單。 

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 了解如何太[使用 StorSimple Snapshot Manager toocreate 及管理磁碟區群組](storsimple-snapshot-manager-manage-volume-groups.md)。

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
