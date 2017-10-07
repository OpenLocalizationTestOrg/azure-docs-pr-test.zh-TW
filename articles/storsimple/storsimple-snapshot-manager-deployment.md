---
title: "aaaDeploy StorSimple Snapshot Manager |Microsoft 文件"
description: "了解 toodownload 並安裝 hello StorSimple Snapshot Manager MMC 嵌入式管理單元來管理 StorSimple 資料保護和備份功能。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>部署 StorSimple Snapshot Manager MMC 嵌入式管理單元的 hello

## <a name="overview"></a>概觀
hello StorSimple Snapshot Manager 是 Microsoft Management Console (MMC) 嵌入式管理單元，可簡化資料保護和備份管理在 Microsoft Azure StorSimple 環境中。 利用 StorSimple Snapshot Manager，您可以管理 Microsoft Azure StorSimple 內部部署和雲端儲存體，就好像是完全整合的儲存系統，並藉此簡化備份和還原程序並降低成本。 

本教學課程描述組態需求，以及安裝、移除及升級 StorSimple Snapshot Manager 的程序。

> [!NOTE]
> * 您無法使用 StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple 虛擬陣列 （也稱為 StorSimple 內部部署虛擬裝置）。
> * 如果您計劃您的 StorSimple 裝置 tooinstall StorSimple Update 2，可確定 toodownload hello 最新版的 StorSimple Snapshot Manager，並將它安裝**安裝 StorSimple Update 2 之前**。 hello 最新版本的 StorSimple Snapshot Manager 的回溯相容性，以及適用於所有的 Microsoft Azure StorSimple 的發行版本。 如果您使用 hello 舊版的 StorSimple Snapshot Manager，您必須 tooupdate it （您不需要 toouninstall hello 先前版本再安裝新版本的 hello）。


## <a name="storsimple-snapshot-manager-installation"></a>StorSimple Snapshot Manager 安裝
StorSimple Snapshot Manager 可以安裝在執行 hello Windows Server 2008 R2 SP1、 Windows Server 2012 或 Windows Server 2012 R2 作業系統的電腦上。 在執行 Windows 2008 R2 的伺服器上，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0。

您安裝或升級 hello StorSimple Snapshot Manager 嵌入式管理單元 hello Microsoft Management Console (MMC) 之前，請確定該 hello Microsoft Azure StorSimple 裝置及主機伺服器已正確設定。

## <a name="configure-prerequisites"></a>設定必要條件
hello 下列步驟提供的組態工作的高階概觀，您必須完成才能安裝 hello StorSimple Snapshot Manager。 如需完整的 Microsoft Azure StorSimple 組態和安裝資訊，包括系統需求和逐步指示，請參閱 [部署您的內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。

> [!IMPORTANT]
> 在開始之前，檢閱 hello[部署組態檢查清單](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist)和[部署必要條件](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)中[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>安裝 StorSimple Snapshot Manager 之前
1. 打開包裝、 裝載和連接 hello Microsoft Azure StorSimple 裝置中所述[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。
2. 請確定您的主機電腦正在執行下列作業系統的 hello 的其中一個：
   
   * Windows Server 2008 R2 (在執行 Windows 2008 R2 的伺服器上，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     StorSimple 虛擬裝置 hello 主機必須是 Microsoft Azure 虛擬機器。
3. 請確定您符合所有的 hello Microsoft Azure StorSimple 設定需求。 如需詳細資訊，請移至太[部署必要條件](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites)。
4. 連接 hello 裝置 toohello 主機並執行 hello 初始設定。 如需詳細資訊，請移至太[部署步驟](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps)。
5. Hello 裝置上建立磁碟區、 將它們指派 toohello 主機，並確認該 hello 主機可以裝載和使用它們。 StorSimple Snapshot Manager 支援下列類型的磁碟區的 hello:
   
   * 基本磁碟區
   * 簡單磁碟區
   * 動態磁碟區
   * 鏡像動態磁碟區 (RAID 1)
   * 叢集共用磁碟區
     
     Hello StorSimple 裝置或 StorSimple 虛擬裝置上建立磁碟區的相關資訊，請太[步驟 6： 建立磁碟區](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume)，請在[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。

## <a name="install-a-new-storsimple-snapshot-manager"></a>安裝新的 StorSimple Snapshot Manager
安裝 StorSimple Snapshot Manager 之前, 請確定您建立 hello StorSimple 裝置或 StorSimple 虛擬裝置的 hello 磁碟區會掛接、 初始化，且格式中所述[設定必要條件](#configure-prerequisites)。

> [!IMPORTANT]
> * StorSimple 虛擬裝置 hello 主機必須是 Microsoft Azure 虛擬機器。 
> * hello 主機必須執行 Windows 2008 R2、 Windows Server 2012 或 Windows Server 2012 R2。 如果您的伺服器執行 Windows Server 2008 R2，您也必須安裝 Windows Server 2008 SP1 和 Windows Management Framework 3.0。
> * 您可以連接 hello 裝置 tooStorSimple Snapshot Manager 之前，您必須設定從 hello 主機 toohello StorSimple 裝置的 iSCSI 連線。

請遵循這些步驟 toocomplete StorSimple Snapshot Manager 的全新安裝。 如果您要安裝升級，請移至太[升級或重新安裝 StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager)。

* 步驟 1：安裝 StorSimple Snapshot Manager 
* 步驟 2: StorSimple Snapshot Manager tooa 裝置連線 
* 步驟 3： 確認 hello 連線 toohello 裝置 

### <a name="step-1-install-storsimple-snapshot-manager"></a>步驟 1：安裝 StorSimple Snapshot Manager
使用下列步驟 tooinstall StorSimple Snapshot Manager hello。

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall StorSimple Snapshot Manager
1. 下載 hello StorSimple Snapshot Manager 軟體 (跳過[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) hello Microsoft 下載中心中) 並將它儲存在本機 hello 主機上。
2. 在檔案總管 中，hello 壓縮的資料夾，以滑鼠右鍵按一下，然後按一下**擷取所有**。
3. 在 hello**解壓縮壓縮 (Zipped) 資料夾**視窗中的，於 hello**選取目的地並解壓縮檔案**方塊中，輸入或瀏覽您要擷取的 toofile toobe toohello 路徑。
   
    > [!IMPORTANT]
    > 您必須安裝 StorSimple Snapshot Manager hello c： 磁碟機上。
    
4. 選取 hello**顯示解壓縮的檔案時完成**核取方塊，然後**擷取**。
   
    ![解壓縮檔案對話方塊](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Hello 解壓縮完成時，會開啟 hello 目的地資料夾。 按兩下 hello 應用程式安裝圖示會出現在 hello 目的地資料夾。
6. 當 hello**安裝成功**訊息出現時，按一下**關閉**。 您應該在桌面上會看到 hello StorSimple Snapshot Manager 圖示。
   
    ![桌面圖示](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>步驟 2: StorSimple Snapshot Manager tooa 裝置連線
使用下列步驟 tooconnect StorSimple Snapshot Manager tooa StorSimple 裝置 hello。

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect StorSimple Snapshot Manager tooa 裝置
1. 按一下桌面上的 hello StorSimple Snapshot Manager 圖示。 hello StorSimple Snapshot Manager 視窗隨即出現。 hello 視窗包含**範圍** 窗格中，**結果** 窗格中，和**動作**窗格。 
   
    ![StorSimple Snapshot Manager 使用者介面](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * hello**範圍**窗格 （hello 左窗格） 包含組織樹狀結構中的節點清單。 您可以展開一些節點 tooselect 檢視或特定的資料相關的 toothat 節點。 按一下 hello 箭號圖示 tooexpand 或摺疊節點。 以滑鼠右鍵按一下項目在 hello**範圍**窗格 toosee 該項目的可用動作的清單。
   * hello**結果**窗格 （hello 中央窗格） 包含 hello 節點、 檢視表或您在 hello 中選取的資料相關的詳細的狀態資訊**範圍**窗格。
   * hello**動作**窗格會列出您可以在 hello 節點、 檢視表或您在 hello 中選取的資料執行的 hello 作業**範圍**窗格。
     
     Hello StorSimple Snapshot Manager 使用者介面的完整說明，請參閱[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。
2. 在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**裝置**節點，然後再按一下**設定裝置**。 hello**設定裝置** 對話方塊隨即出現。
   
    ![設定裝置](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. 在 hello**裝置**清單方塊中，選取 hello hello Microsoft Azure StorSimple 裝置的虛擬裝置的 IP 位址。 在 hello**密碼**文字方塊中，您建立 hello 裝置 hello Azure 入口網站中的型別 hello StorSimple Snapshot Manager 密碼。 按一下 [確定] 。
4. StorSimple Snapshot Manager 搜尋您所識別的 hello 裝置。 如果使用 hello 裝置，StorSimple Snapshot Manager 就會加入連接。 您可以[確認 hello 連線 toohello 裝置](#to-verify-the-connection)hello 連線的 tooconfirm 成功加入。
   
    如果因為任何原因無法使用 hello 裝置，StorSimple Snapshot Manager 就會傳回錯誤訊息。 按一下**確定**tooclose hello 錯誤訊息，然後按一下**取消**tooclose hello**設定裝置** 對話方塊。
5. 連接 tooa 裝置之後，StorSimple Snapshot Manager 匯入該裝置，設定每個磁碟區群組，前提是 hello 磁碟區群組有相關聯的備份。 不會匯入沒有相關聯備份的磁碟區群組。 此外，不會匯入為磁碟區群組建立的備份原則。 toosee hello 匯入的群組，以滑鼠右鍵按一下 hello 最上層**磁碟區群組**節點 hello**範圍** 窗格中，然後按一下**切換匯入的群組**。

### <a name="step-3-verify-hello-connection-toohello-device"></a>步驟 3： 確認 hello 連線 toohello 裝置
使用下列步驟 tooverify StorSimple Snapshot Manager 是連接的 toohello StorSimple 裝置 hello。

#### <a name="tooverify-hello-connection"></a>tooverify hello 連線
1. 在 [hello**範圍**] 窗格中，按一下 hello**裝置**節點。
   
    ![StorSimple Snapshot Manager 裝置狀態](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. 檢查 hello**結果**窗格： 
   
   * 如果在 hello 裝置圖示上出現綠色指示器和**可用**會出現在 hello**狀態**資料行，然後 hello 裝置已連線。 
   * 如果在 hello 裝置圖示上出現紅色指示器，且無法使用出現在 hello**狀態**資料行，然後 hello 裝置未連線。 
   * 如果**正在重新整理**會出現在 hello**狀態**資料行，然後 StorSimple Snapshot Manager 正在擷取磁碟區群組和連接的裝置相關聯的備份。

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>升級或重新安裝 StorSimple Snapshot Manager
您應該完全解除安裝 StorSimple Snapshot Manager 才能升級或重新安裝 hello 軟體。 

重新安裝 StorSimple Snapshot Manager 之前, 備份 hello 現有 StorSimple Snapshot Manager 資料庫 hello 主機電腦上。 這會儲存 hello 備份原則和組態資訊，以便您可以輕鬆地從備份還原此資料。

如果您要升級或重新安裝 StorSimple Snapshot Manager，請遵循下列步驟：

* 步驟 1：解除安裝 StorSimple Snapshot Manager 
* 步驟 2： 備份 hello StorSimple Snapshot Manager 資料庫 
* 步驟 3： 重新安裝 StorSimple Snapshot Manager 及 hello 資料庫還原 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>步驟 1：解除安裝 StorSimple Snapshot Manager
使用下列步驟 toouninstall StorSimple Snapshot Manager hello。

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall StorSimple Snapshot Manager
1. Hello 主機電腦上，開啟 hello**控制台**，按一下 **程式**，然後按一下**程式和功能**。
2. 在 hello 左窗格中，按一下 **解除安裝或變更程式**。
3. 以滑鼠右鍵按一下 StorSimple Snapshot Manager，然後按一下解除安裝。
4. 這樣會啟動 hello StorSimple Snapshot Manager 安裝程式。 按一下 修改安裝程式，然後按一下解除安裝。
   
   > [!NOTE]
   > 如果有 hello 背景中執行任何 MMC 程序，例如 StorSimple Snapshot Manager 或磁碟管理，hello 解除安裝會失敗，而且您會收到訊息 tooclose MMC 之前的所有執行個體就會嘗試 toouninstall hello 程式。 選取**自動關閉應用程式，並嘗試的 toorestart 它們在安裝後完成**，然後按一下**確定**。
   > 
   > 
5. 當 hello 解除安裝程序完成，**安裝成功**會出現訊息。 按一下 [關閉] 。

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>步驟 2： 備份 hello StorSimple Snapshot Manager 資料庫
使用下列步驟 toocreate hello 和儲存一份 hello StorSimple Snapshot Manager 資料庫。

#### <a name="tooback-up-hello-database"></a>tooback hello 資料庫
1. 停止 Microsoft StorSimple 管理服務的 hello:
   
   1. 啟動伺服器管理員。
   2. 在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。
   3. 在 hello**服務**頁面上，選取**Microsoft StorSimple 管理服務**。
   4. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。
      
        ![停止 hello StorSimple 裝置管理員服務](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. 瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。 
   
   > [!NOTE]
   > ProgramData 是隱藏的資料夾。
  
3. 尋找 hello 類別目錄 XML 檔案，複製 hello 檔案，並存放區 hello 複製在安全的位置或 hello 雲端中。
   
    ![StorSimple 備份目錄檔案](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. 重新啟動 Microsoft StorSimple 管理服務的 hello: 
   
   1. 在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。
   2. 在 hello**服務**頁面上，選取 hello **Microsoft StorSimple 管理服務**e。
   3. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>步驟 3： 重新安裝 StorSimple Snapshot Manager 及 hello 資料庫還原
tooreinstall StorSimple Snapshot Manager，請依照下列中的 hello 步驟[安裝新的 StorSimple Snapshot Manager](#install-a-new-storsimple-snapshot-manager)。 然後，使用下列程序 toorestore hello StorSimple Snapshot Manager 資料庫的 hello。

#### <a name="toorestore-hello-database"></a>toorestore hello 資料庫
1. 停止 Microsoft StorSimple 管理服務的 hello:
   
   1. 啟動伺服器管理員。
   2. 在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。
   3. 在 hello**服務**頁面上，選取**Microsoft StorSimple 管理服務**。
   4. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。
2. 瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。
   
   > [!NOTE]
   > ProgramData 是隱藏的資料夾。
   > 
   > 
3. 刪除 hello 類別目錄 XML 檔案，然後您稍早儲存的 hello 版本取代它。
4. 重新啟動 Microsoft StorSimple 管理服務的 hello: 
   
   1. 在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。
   2. 在 hello**服務**頁面上，選取**Microsoft StorSimple 管理服務**。
   3. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。

## <a name="next-steps"></a>後續步驟
* toolearn 更多關於 StorSimple Snapshot Manager，跳過[什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md)。
* 進一步了解 hello StorSimple Snapshot Manager 使用者介面，toolearn 移過[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。
* 進一步了解使用 StorSimple Snapshot Manager，toolearn 移過[使用 StorSimple Snapshot Manager tooadminister 您於 StorSimple 解決方案](storsimple-snapshot-manager-admin.md)。

