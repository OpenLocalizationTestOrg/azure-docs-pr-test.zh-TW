---
title: "設定 Windows 系統狀態 tooAzure aaaBack |Microsoft 文件"
description: "了解 tooback 的 Windows Server 和/或 Windows 電腦 tooAzure hello 系統狀態。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "如何 toobackup;如何設定; tooback備份檔案和資料夾"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>在 Resource Manager 部署中備份 Windows 系統狀態
本文說明如何 tooback 您 Windows Server 的系統狀態 tooAzure。 它是教學課程的預定的 toowalk 您透過 hello 基本概念。

如果您想 tooknow 深入了解 Azure 備份，請閱讀本[概觀](backup-introduction-to-azure-backup.md)。

如果您沒有 Azure 訂用帳戶，請建立 [免費帳戶](https://azure.microsoft.com/free/) ，以便存取任何 Azure 服務。

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
您的檔案及資料夾 tooback，您需要 toocreate hello toostore hello 資料所在的區域中的復原服務保存庫。 您也需要的 toodetermine 方式複寫儲存體。

### <a name="toocreate-a-recovery-services-vault"></a>toocreate 復原服務保存庫
1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。
2. 在 hello 中樞功能表中，按一下 [**更多服務**hello] 清單中的資源，在輸入**復原服務**按一下**復原服務保存庫**。

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    如果 hello 訂用帳戶中沒有復原服務保存庫，則會列出 hello 保存庫。
3. 在 hello**復原服務保存庫**功能表上，按一下 **新增**。

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. 如**名稱**，輸入好記名稱 tooidentify hello 保存庫。 hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。 輸入包含 2 到 50 個字元的名稱。 該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。

5. 在 hello**訂用帳戶**區段中，使用 hello 下拉式功能表 toochoose hello Azure 訂用帳戶。 如果您使用只有一個訂用帳戶時，會出現該訂用帳戶，所以您可以跳 toohello 下一個步驟。 如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。 只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。

6. 在 hello**資源群組**> 一節：

    * 選取**建立新**如果您想 toocreate 資源群組。
    或
    * 選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。

  完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。

7. 按一下**位置**hello 保存庫的 tooselect hello 地理區域。 這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。

8. 在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。

    可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。 監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。 一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。 在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。

    ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。

### <a name="set-storage-redundancy-for-hello-vault"></a>設定儲存體備援 hello 保存庫
當您建立的復原服務保存庫時，請確定儲存體備援設定的 hello 您想要的方式。

1. 從 hello**復原服務保存庫**刀鋒視窗中，按一下 hello 新的保存庫。

    ![從 hello 復原服務保存庫清單中選取 hello 新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    當您選取 hello 保存庫時，hello**復原服務保存庫**刀鋒視窗縮小及 hello 設定 刀鋒視窗 (*hello 頂端具有 hello hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗開啟。

    ![檢視新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. 在 hello 新的保存庫的設定 刀鋒視窗中，使用 hello 垂直投影片 tooscroll toohello 管理 區段中，關閉，然後按一下**備份基礎結構**。
    hello 備份基礎結構刀鋒視窗隨即開啟。
3. 在 hello 備份基礎結構刀鋒視窗中，按一下 **備份設定**tooopen hello**備份設定**刀鋒視窗。

    ![設定新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. 選擇您的保存庫的 hello 適當的儲存體複寫選項。

    ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    根據預設，保存庫具有異地備援儲存體。 如果您使用 Azure 做為備份的主要儲存體端點時，繼續 toouse**異地備援**。 如果您不使用 Azure 做為備份的主要儲存體端點，然後選擇 **本機備援**，進而降低 hello Azure 儲存體成本。 在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。

您已建立了保存庫，接著請設定它來備份 Windows 系統狀態。

## <a name="configure-hello-vault"></a>設定 hello 保存庫
1. 在復原服務保存庫刀鋒視窗 （適用於 hello 保存庫中您剛建立），hello hello 開始使用 > 一節中，按一下**備份**，然後在 hello**開始使用備份**刀鋒視窗中，選取**備份目標**。

    ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    hello**備份目標**刀鋒視窗隨即開啟。

    ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. 從 hello**其中執行您的工作負載？**下拉式選單中，選取**內部**。

    因為您的 Windows Server 或 Windows 電腦是不在 Azure 中的實體電腦，所以您選擇 [內部部署]。

3. 從 hello**怎麼辦想 toobackup？**功能表上，選取**系統狀態**，按一下**確定**。

    ![設定檔案和資料夾](./media/backup-azure-system-state/backup-goal-system-state.png)

    之後按一下 確定 核取記號會出現 下一步太**備份目標**，和 hello**準備基礎結構**刀鋒視窗隨即開啟。

    ![已設定備份目標，接下來是準備基礎結構](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. 在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載適用於 Windows Server 的代理程式或 Windows 用戶端**。

    ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    如果您使用 Windows Server 基本項目，然後選擇 toodownload hello 代理程式的 Windows Server 不可或缺。 快顯功能表會提示您 toorun 或儲存 MARSAgentInstaller.exe。

    ![MARSAgentInstaller dialog](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. 在 hello 下載快顯功能表上，按一下 **儲存**。

    根據預設，hello **MARSagentinstaller.exe** tooyour Downloads 資料夾儲存檔案。 Hello 安裝程式完成時，您會看到快顯視窗，詢問您想 toorun hello 安裝程式，或開啟 hello 資料夾。

    ![準備基礎結構](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    您無須 tooinstall hello 代理程式。 您已下載 hello 保存庫認證之後，您可以安裝 hello 代理程式。

6. 在 hello**準備基礎結構**刀鋒視窗中，按一下 **下載**。

    ![下載保存庫認證](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    hello 保存庫認證下載 tooyour 下載 資料夾。 Hello 保存庫認證完成下載之後，您會看到快顯視窗，詢問您想 tooopen 或儲存 hello 認證。 按一下 [儲存] 。 如果您不小心按**開啟**、 讓 hello 對話方塊中嘗試 tooopen hello 保存庫認證失敗。 您無法開啟 hello 保存庫認證。 繼續 toohello 下一個步驟。 hello 保存庫認證是在 hello 下載 資料夾中。   

    ![保存庫認證下載完成](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>安裝並註冊 hello 代理程式

> [!NOTE]
> 透過 hello Azure 入口網站啟用備份尚無法使用。 使用 hello Microsoft Azure Recovery Services Agent tooback Windows 伺服器系統狀態。
>

1. 找出並按兩下 hello **MARSagentinstaller.exe** hello 下載資料夾 （或其他已儲存的位置）。

    hello 安裝程式會提供一系列的訊息，擷取安裝，並註冊 hello 復原服務代理程式。

    ![執行復原服務代理安裝程式的認證](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. 完成 hello Microsoft Azure Recovery Services Agent 安裝精靈。 您需要 toocomplete hello 精靈:

   * 選擇 hello 安裝和快取資料夾的位置。
   * 提供 proxy 伺服器資訊，如果您使用 proxy 伺服器 tooconnect toohello 網際網路。
   * 如果您使用已驗證的 Proxy，請提供您的使用者名稱和密碼詳細資料。
   * 提供 hello 下載保存庫認證
   * 將 hello 加密複雜密碼儲存在安全的位置。

     > [!NOTE]
     > 如果您遺失或忘記 hello 複雜密碼時，Microsoft 無法協助復原 hello 備份資料。 將 hello 檔案儲存在安全的位置。 它是必要的 toorestore 備份。
     >
     >

hello 代理程式現在已安裝，且您的電腦已註冊的 toohello 保存庫。 正在準備 tooconfigure，並將備份排程。

## <a name="back-up-windows-server-system-state-preview"></a>備份 Windows Server 系統狀態 (預覽)
hello 初始備份包含三個工作：

* 啟用系統狀態備份使用 hello Azure Backup agent
* Hello 備份排程
* 備份檔案和資料夾進行 hello 第一次

toocomplete hello 初始備份、 使用 hello Microsoft Azure 復原服務代理程式。

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>使用 hello Azure Backup agent tooenable 系統狀態備份

1. PowerShell 工作階段中執行下列命令 toostop hello Azure 備份引擎 hello。

  ```
  PS C:\> Net stop obengine
  ```

2. 開啟 Windows 登錄 hello。

  ```
  PS C:\> regedit.exe
  ```

3. 加入下列登錄機碼以 hello hello 指定 DWord 值。

  | 登錄路徑 | 登錄機碼 | DWord 值 |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. 藉由執行下列命令，在提升權限的命令提示字元中的 hello，重新啟動 hello 備份引擎。

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>tooschedule hello 備份工作

1. 開啟 hello Microsoft Azure Recovery Services agent。 您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。

    ![啟動 hello Azure 復原服務代理程式](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. 在 hello 復原服務代理程式，按一下 **排程備份**。

    ![Windows Server 備份排程](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. 在 [hello 上開始使用 hello 排程備份精靈] 頁面中，按一下**下一步**。

4. 在 hello 選取項目 tooBackup 頁面上，按一下 **新增的項目**。

5. 選取 系統狀態，然後按一下確定。

6. 按一下 [下一步] 。

7. hello 系統狀態備份和保留排程會自動設定 tooback 總每個星期天下午 9:00 的當地時間，並 hello 保留週期設 too60 天。

   > [!NOTE]
   > 系統會自動設定系統狀態的備份和保留原則。 如果您將備份檔案和資料夾此外 toohello Windows 伺服器系統狀態，指定唯一的檔案備份，從 hello 精靈的 hello 備份和保留原則。 
   >

8. 在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。

9. Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>Windows 伺服器系統狀態的 tooback hello 第一次

1. 確定 Windows Server 沒有需要重新啟動的擱置中更新。

2. 在 hello 復原服務代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。

    ![立即備份 Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. 在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。 然後按一下 [備份] 。

4. 按一下**關閉**tooclose hello 精靈。 如果您在 hello 備份程序完成之前關閉 hello 精靈，hello 精靈會繼續 toorun hello 背景。

5. 如果您將備份檔案和資料夾在伺服器上另外 toohello Windows 伺服器系統狀態，hello 立即備份精靈會只備份檔案。 tooperform 臨機操作的系統狀態備份，請使用下列 PowerShell 命令的 hello:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。

  ![IR 已完成](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>常見問題集

hello 以下問題和解答提供補充資訊。

### <a name="what-is-hello-staging-volume"></a>什麼是 hello 暫存磁碟區？

hello 暫存磁碟區表示 hello hello 原生功能，Windows Server Backup 要分階段 hello 系統狀態備份的中間位置。 Azure 備份代理程式則會壓縮及加密此中繼備份並將它透過安全的 HTTPS 通訊協定 toohello 設定復原服務保存庫。 **我們強烈建議您在非 Windows 作業系統磁碟區建立 hello 暫存磁碟區。如果您觀察系統狀態備份發生問題時，檢查您的暫存磁碟區的 hello 位置是 hello 的第一個疑難排解步驟。** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>如何變更 hello hello Azure Backup agent 中指定的暫存磁碟區路徑？

根據預設 hello 暫存磁碟區位於 hello 快取資料夾。 

1. toochange 這個位置，使用下列命令 （在提升權限的命令提示字元） 的 hello:
  ```
  PS C:\> Net stop obengine
  ```

2. 然後更新 hello 遵循 hello 路徑 toohello 新暫存磁碟區的資料夾與登錄項目。

  |登錄路徑|登錄機碼|值|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | 新的暫存磁碟區位置 |

hello 臨時區域路徑會區分大小寫，而且必須是 hello 完全相同的大小寫為項目存在 hello 伺服器上。 

3. 一旦變更 hello 暫存磁碟區路徑，請重新啟動 hello 備份引擎：
  ```
  PS C:\> Net start obengine
  ```
4. toopick 出 hello 變更路徑，請開啟 hello Microsoft Azure 復原服務代理程式觸發程序的系統狀態的臨機操作備份。

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>為什麼會預設保留設定 too60 天 hello 系統狀態？

系統狀態備份的 hello 有用的生命週期是 hello 與 hello 」 標記存留時間 」 設定 hello Windows Server Active Directory 角色相同。 hello 標記存留期項目的 hello 預設值是 60 天。 這個值可以在 hello 目錄服務 (NTDS) 組態物件上設定。

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>如何變更 hello 預設備份和系統狀態的保留原則？

toochange hello 預設備份和保留原則對於系統狀態：
1. 停止 hello 備份引擎。 執行下列命令，從提升權限的命令提示字元的 hello。

  ```
  PS C:\> Net stop obengine
  ```

2. 加入或更新 hello 遵循 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider 中登錄索引鍵的項目。

  |登錄名稱|說明|值|
  |-------------|-----------|-----|
  |SSBScheduleTime|使用的 tooconfigure hello hello 備份時間。 預設值為當地時間下午 9 點。|DWord：格式為 HHMM (十進位)，例如用 2130 代表當地時間下午 9:30|
  |SSBScheduleDays|使用的 tooconfigure hello 天系統狀態備份時必須在 hello 執行指定的時間。 獨立的數字指定 hello 一週天數。 0 代表星期日、1 代表星期一，依此類推。 預設的備份日是星期日。|Hello 週 toorun 備份 1230年例如排定備份在上星期一、 星期二、 星期三與星期日 （十進位） 的 DWord： 天數。|
  |SSBRetentionDays|使用的 tooconfigure hello 天 tooretain 備份。 預設值為 60。 允許的最大值為 180。|DWord： 天 tooretain 備份 （十進位）。|

3. 使用下列命令 toorestart hello 備份引擎 hello。
    ```
    PS C:\> Net start obengine
    ```

4. 開啟 hello Microsoft 復原服務代理程式。

5. 按一下**排程備份**，然後按一下**下一步**直至您看見 hello 反映的變更。

6. 按一下**完成**tooapply hello 變更。


## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。

## <a name="next-steps"></a>後續步驟
* 詳細了解如何 [備份 Windows 電腦](backup-configure-vault.md)。
* 現在您已備份好檔案和資料夾，接下來您可以 [管理您的保存庫和伺服器](backup-azure-manage-windows-server.md)。
* 如果您需要 toorestore 備份，請使用本文章太[還原檔案 tooa Windows 機器](backup-azure-restore-windows-server.md)。
