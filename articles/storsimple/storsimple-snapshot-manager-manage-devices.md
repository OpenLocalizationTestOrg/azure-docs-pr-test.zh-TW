---
title: "aaaManage 裝置與 StorSimple Snapshot Manager |Microsoft 文件"
description: "描述如何 toouse hello StorSimple Snapshot Manager MMC 嵌入式管理單元 tooconnect 和管理 StorSimple 裝置。"
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>使用 StorSimple Snapshot Manager tooconnect 和管理 StorSimple 裝置
## <a name="overview"></a>概觀
您可以使用節點中 hello StorSimple Snapshot Manager**範圍**窗格 tooverify 匯入的 StorSimple 裝置資料和重新整理已連線的存放裝置。 此外，當您按一下 hello**裝置** 節點，您可以看到一份連接的裝置和對應的狀態資訊在 hello**結果**窗格。

![連接的裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**圖 1：StorSimple Snapshot Manager 連接的裝置** 

取決於您**檢視**選取項目、 hello**結果** 窗格會顯示 hello 下列每個裝置的相關資訊。 (如需有關如何設定檢視的詳細資訊，請移至太[檢視 功能表](storsimple-use-snapshot-manager.md#view-menu)。

| 結果資料行 | 說明 |
|:--- |:--- |
| 名稱 |hello hello 裝置 hello Azure 傳統入口網站中的設定名稱 |
| 模型 |hello 裝置 hello 型號號碼 |
| 版本 |hello 新版 hello hello 裝置上安裝的軟體 |
| 狀態 |Hello 裝置是否可供使用 |
| 上次同步處理 |日期和時間時 hello 裝置上次同步處理 |
| 序號 |hello 裝置 hello 序號 |

如果您以滑鼠右鍵按一下 hello**裝置**hello 中的節點**範圍** 窗格中，您可以選取從 hello 下列動作：

* 新增或更換裝置
* 連接裝置並確認匯入
* 重新整理已連接的裝置

如果您按一下 hello**裝置**hello 中的節點，然後以滑鼠右鍵按一下裝置名稱**結果** 窗格中，您可以選取從 hello 下列動作：

* 驗證裝置
* 檢視裝置詳細資料
* 重新整理裝置
* 刪除裝置組態
* 變更裝置密碼

> [!NOTE]
> 所有這些動作也會提供在 hello**動作**窗格。


本教學課程說明如何 toouse StorSimple Snapshot Manager tooconnect 及管理裝置，並執行下列工作的 hello:

* 新增或更換裝置
* 連接裝置並確認匯入
* 重新整理已連接的裝置
* 驗證裝置
* 檢視裝置詳細資料
* 重新整理個別裝置
* 刪除裝置組態
* 變更過期的裝置密碼
* 更換故障的裝置

> [!NOTE]
> 如需使用 hello StorSimple Snapshot Manager 介面的一般資訊，請移太[StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。


## <a name="add-or-replace-a-device"></a>新增或更換裝置
使用下列程序 tooadd hello 或取代 StorSimple 裝置。

#### <a name="tooadd-or-replace-a-device"></a>tooadd 或取代裝置
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍**窗格中，以滑鼠右鍵按一下 hello**裝置**節點，然後再按一下**設定裝置**。 hello**設定裝置** 對話方塊隨即出現。
   
    ![設定 StorSimple 裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. 在 hello**裝置**下拉式清單方塊中，選取 hello hello 裝置或虛擬裝置的 IP 位址。 
4. 在 hello**密碼**文字方塊中，您建立 hello 裝置 hello Azure 傳統入口網站中的型別 hello StorSimple Snapshot Manager 密碼。 按一下 [確定] 。 StorSimple Snapshot Manager 搜尋您所識別的 hello 裝置。 
   
   * 如果使用 hello 裝置，StorSimple Snapshot Manager 就會加入連接。
   * 如果因為任何原因無法使用 hello 裝置，StorSimple Snapshot Manager 就會傳回錯誤訊息。 按一下**確定**tooclose hello 錯誤訊息，然後按一下**取消**tooclose hello**設定裝置** 對話方塊。

## <a name="connect-a-device-and-verify-imports"></a>連接裝置並確認匯入
使用下列程序 tooconnect StorSimple 裝置 hello，並確認具備相關聯備份任何現有磁碟區群組匯入。

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect 裝置並驗證匯入
1. tooconnect 裝置 tooStorSimple Snapshot Manager 遵循 hello 指示中新增或取代裝置。 當它連接 tooa 裝置時，StorSimple Snapshot Manager 回應，如下所示：
   
   * 如果因為任何原因無法使用 hello 裝置，StorSimple Snapshot Manager 就會傳回錯誤訊息。 
   
   * 如果使用 hello 裝置，StorSimple Snapshot Manager 就會加入連接。 當您選取 hello 裝置時，它會出現在 hello**結果** 窗格中，而 hello 狀態欄位表示該 hello 裝置為**可用**。 StorSimple Snapshot Manager 匯入設定 hello 裝置的任何磁碟區群組，前提是 hello 磁碟區群組有相關聯的備份。 不會匯入備份原則。 不會匯入沒有相關聯備份的磁碟區群組。
2. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
3. 以滑鼠右鍵按一下 hello 中的最上層節點 hello**範圍** 窗格中，然後再按一下**切換匯入顯示**。
   
    ![選取 [切換匯入顯示]](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. hello**切換匯入顯示**磁碟區群組及備份時將會出現對話方塊，顯示 hello hello 狀態匯入。 按一下 [確定] 。

Hello 磁碟區群組及備份已順利匯入之後，您可以使用 StorSimple Snapshot Manager toomanage 它們，就如同您管理磁碟區群組及您建立及設定 StorSimple Snapshot Manager 使用的備份。 

## <a name="refresh-connected-devices"></a>重新整理已連接的裝置
使用下列程序 toosynchronize hello 連接 StorSimple 裝置的 StorSimple Snapshot Manager hello。

#### <a name="toorefresh-connected-devices"></a>toorefresh 連接的裝置
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下**裝置**，然後按一下**重新整理裝置**。 這會同步處理 hello 連接裝置與 StorSimple Snapshot Manager，讓您可以檢視 hello 磁碟區群組及備份，包括任何最近新增項目。 
   
    ![重新整理 hello StorSimple 裝置](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

hello**重新整理裝置**動作會擷取任何新的磁碟區群組及任何相關聯的備份從連接的裝置。 不同於 hello**重新掃描磁碟區**動作供 hello**磁碟區** 節點，**重新整理裝置**不會還原 hello 備份登錄。

## <a name="authenticate-a-device"></a>驗證裝置
使用下列程序 tooauthenticate StorSimple 裝置的 StorSimple Snapshot Manager hello。

#### <a name="tooauthenticate-a-device"></a>tooauthenticate 裝置
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，按一下 **裝置**。
3. 在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**驗證**。
4. hello**驗證** 對話方塊隨即出現。 輸入 hello 裝置密碼，然後再按一下**確定**。
   
    ![[驗證] 對話方塊](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>檢視裝置詳細資料
使用下列程序 tooview hello 詳細資料的 StorSimple 裝置 hello，並視需要重新同步處理 hello 裝置與 StorSimple Snapshot Manager。

#### <a name="tooview-and-resynchronize-device-details"></a>tooview 和重新同步處理裝置詳細資料
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，按一下 **裝置**。
3. 在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**詳細資料**。

4.hello**裝置詳細資料** 對話方塊隨即出現。 此方塊會顯示 hello 名稱、 模型、 版本、 序號、 狀態、 目標 iSCSI 合格名稱 (IQN) 及上次同步處理日期和時間。

* 按一下**重新同步處理**toosynchronize hello 裝置。
* 按一下**確定**或**取消**tooclose hello 對話方塊。
  
  ![裝置詳細資料](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>重新整理個別裝置
使用下列程序 tooresynchronize 個別的 StorSimple 裝置的 StorSimple Snapshot Manager hello。

#### <a name="toorefresh-a-device"></a>toorefresh 裝置
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。 
2. 在 hello**範圍** 窗格中，按一下 **裝置**。 
3. 在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**重新整理裝置**。 此同步處理裝置 hello 與 StorSimple Snapshot Manager。

## <a name="delete-a-device-configuration"></a>刪除裝置組態
使用下列程序 toodelete 個別的 StorSimple 裝置設定 StorSimple Snapshot Manager 從 hello。

#### <a name="toodelete-a-device-configuration"></a>toodelete 裝置組態
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，按一下 **裝置**。 
3. 在 hello**結果**hello hello 裝置名稱，以滑鼠右鍵按一下窗格中，然後再按一下**刪除**。 
4. hello 下訊息隨即出現。 按一下**是**toodelete hello 組態，或按一下**否**toocancel hello 刪除。
   
    ![刪除裝置組態](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>變更過期的裝置密碼
您必須輸入密碼 tooauthenticate StorSimple 裝置的 StorSimple Snapshot Manager。 當您使用 hello Windows PowerShell 介面 tooset hello 裝置時，您可以設定這個密碼。 不過，hello 密碼可能會過期。 如果發生這種情況，您可以使用 hello Azure 傳統入口網站 toochange hello 密碼。 然後，因為 hello 裝置已設定 StorSimple Snapshot Manager 中的 hello 密碼過期之前，您必須重新驗證 hello 裝置在 StorSimple Snapshot Manager。

#### <a name="toochange-hello-expired-password"></a>toochange hello 過期的密碼
1. 在 hello Azure 傳統入口網站，開始 hello StorSimple Manager 服務。
2. 按一下**裝置** > **設定**hello 裝置。
3. 捲動 toohello StorSimple Snapshot Manager > 一節。 輸入 14 或 15 個字元的密碼。 請確定該 hello 密碼包含大寫、 小寫、 數字及特殊字元的混合。
4. 重新輸入 hello 密碼 tooconfirm 它。
5. 按一下**儲存**hello hello 頁底端。

#### <a name="toore-authenticate-hello-device"></a>toore-驗證 hello 裝置
1. 啟動 StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，按一下 **裝置**。 設定裝置的清單會出現在 hello**結果**窗格。
3. 選取裝置 hello、 按一下滑鼠右鍵，然後按一下**驗證**。
4. 在 hello**驗證**視窗中，輸入 hello 新密碼。
5. 選取 hello 裝置，以滑鼠右鍵按一下，並選取**重新整理裝置**。 此同步處理裝置 hello 與 StorSimple Snapshot Manager。

## <a name="replace-a-failed-device"></a>更換故障的裝置
如果 StorSimple 裝置故障，並由備用 （容錯移轉） 裝置，使用下列步驟 tooconnect 的 hello 取代 toohello 新裝置和檢視 hello 相關聯的備份。

#### <a name="tooconnect-tooa-new-device-after-failover"></a>在容錯移轉之後 tooconnect tooa 新裝置
1. 重新設定 hello iSCSI 連線 toohello 新裝置。 如需相關指示，請移至太 」 步驟 7： 掛接、 初始化、 和格式的磁碟區 」 中[部署在內部部署 StorSimple 裝置](storsimple-8000-deployment-walkthrough-u2.md)。

> [!NOTE]
> 如果新 StorSimple 裝置 hello 具有舊 hello hello 相同的 IP 位址，您可能會無法 tooconnect hello 舊組態。


1. 停止 Microsoft StorSimple 管理服務的 hello:
   
   1. 啟動伺服器管理員。
   2. 在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。
   3. 在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。
   4. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下 **停止 hello 服務**。
2. 移除 hello 組態資訊相關的 toohello 舊裝置：
   
   1. 在檔案總管 中，瀏覽 tooC:\ProgramData\Microsoft\StorSimple\BACatalog。
   2. 刪除 hello BACatalog 資料夾中的 hello 檔案。
3. 重新啟動 Microsoft StorSimple 管理服務的 hello:
   
   1. 在 hello 伺服器管理員儀表板上 hello**工具**功能表上，選取**服務**。
   2. 在 hello**服務**視窗中，選取 hello **Microsoft StorSimple 管理服務**。
   3. 在 hello 右窗格中，在**Microsoft StorSimple 管理服務**，按一下  **hello 服務重新啟動**。
4. 啟動 StorSimple Snapshot Manager。
5. tooconfigure hello 新 StorSimple 裝置，請完成 hello 步驟在步驟 2： 連接 StorSimple 裝置中的[部署 StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md)。
6. 以滑鼠右鍵按一下 hello 中的最上層節點 hello**範圍**窗格 (StorSimple Snapshot Manager hello 範例，)，然後按一下**切換匯入顯示**。 
7. Hello 匯入磁碟區群組，並備份會顯示在 StorSimple Snapshot Manager 時，就會出現訊息。 按一下 [確定] 。

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 了解如何太[使用 StorSimple Snapshot Manager tooview 及管理磁碟區](storsimple-snapshot-manager-manage-volumes.md)。

