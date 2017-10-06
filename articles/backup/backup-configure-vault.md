---
title: "檔案及資料夾 aaaUse Azure 備份代理程式 tooback |Microsoft 文件"
description: "使用 Windows 檔案和資料夾 tooAzure 向上 hello Microsoft Azure 備份代理程式 tooback。 建立復原服務保存庫、 安裝 hello 備份代理程式、 定義 hello 備份原則，並執行 hello 初始備份 hello 檔案及資料夾。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "備份保存庫；備份 Windows Server；備份Windows；"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>備份 Windows Server 或用戶端 tooAzure，使用 hello Resource Manager 部署模型
> [!div class="op_single_selector"]
> * [Azure 入口網站](backup-configure-vault.md)
> * [傳統入口網站](backup-configure-vault-classic.md)
>
>

本文說明如何使用 Azure 備份您的 Windows Server （或 Windows 用戶端） tooback 檔案和資料夾 tooAzure hello Resource Manager 部署模型。

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![備份程序步驟](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>開始之前
伺服器或用戶端 tooAzure tooback，您需要 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫
復原服務保存庫是儲存所有的 hello 備份和復原點建立一段時間的實體。 hello 復原服務保存庫也包含 hello 套用的備份原則 toohello 受保護檔案和資料夾。 當您建立的復原服務保存庫時，您應該也選取 hello 適當的儲存體備援選項。

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

    * 選取**建立新**如果您想 toocreate 新的資源群組。
    或
    * 選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。

  完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。

7. 按一下**位置**hello 保存庫的 tooselect hello 地理區域。 這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。

8. 在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。

  可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。 監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。 一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。 在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。

  ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。


### <a name="set-storage-redundancy"></a>設定儲存體備援
首次建立復原服務保存庫時會決定儲存體的複寫方式。

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

既然您已建立保存庫，請下載和安裝 hello Microsoft Azure 復原服務代理程式、 下載保存庫認證，然後使用這些認證 tooregister hello 代理程式與準備您的基礎結構 tooback 檔案及資料夾hello 保存庫。

## <a name="configure-hello-vault"></a>設定 hello 保存庫

1. 在復原服務保存庫刀鋒視窗 （適用於 hello 保存庫中您剛建立），hello hello 開始使用 > 一節中，按一下**備份**，然後在 hello**開始使用備份**刀鋒視窗中，選取**備份目標**。

  ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  hello**備份目標**刀鋒視窗隨即開啟。 如果之前已經設定的 hello 復原服務保存庫，然後 hello**備份目標**刀鋒視窗隨即開啟，當您按一下**備份**hello 復原服務保存庫刀鋒視窗。

  ![開啟備份目標刀鋒視窗](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. 從 hello**其中執行您的工作負載？**下拉式選單中，選取**內部**。

  因為您的 Windows Server 或 Windows 電腦是不在 Azure 中的實體電腦，所以您選擇 [內部部署]。

3. 從 hello**怎麼辦想 toobackup？**功能表上，選取**檔案和資料夾**，按一下**確定**。

  ![設定檔案和資料夾](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

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
> 透過 hello Azure 入口網站啟用備份尚無法使用。 使用您的檔案及資料夾的 hello Microsoft Azure Recovery Services Agent tooback。
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

## <a name="network-and-connectivity-requirements"></a>網路和連線需求

如果您的電腦/proxy 具有有限的網際網路存取，請確定 hello 機器/proxy 上的防火牆設定已設定的 tooallow hello 下列 Url: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.WindowsAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>建立 hello 備份原則
hello 備份原則時，hello 排程復原點會採取與 hello 的 hello 復原點，就會保留的時間長度。 使用檔案和資料夾的 hello Microsoft Azure 備份代理程式 toocreate hello 備份原則。

### <a name="toocreate-a-backup-schedule"></a>toocreate 備份排程
1. 開啟 hello Microsoft Azure 備份代理程式。 您可以透過在您的電腦中搜尋 **Microsoft Azure 備份**來找出備份。

    ![啟動 hello Azure 備份代理程式](./media/backup-configure-vault/snap-in-search.png)
2. 在 [hello 備份代理程式的**動作**] 窗格中，按一下 [**排程備份**toolaunch hello 排程備份精靈]。

    ![Windows Server 備份排程](./media/backup-configure-vault/schedule-first-backup.png)

3. 在 hello**入門**的 hello 排程備份精靈 頁面上按一下**下一步**。
4. 在 hello**選取項目 tooBackup**頁面上，按一下**新增的項目**。

  hello 選取項目 對話方塊隨即開啟。

5. 選取 hello 檔案和資料夾，您想 tooprotect，然後再按一下**確定**。
6. 在 hello**選取項目 tooBackup**頁面上，按一下**下一步**。
7. 在 hello**指定備份排程**頁面上，指定 hello 備份排程，以及按一下**下一步**。

    您可以排程每日 (一天最多三次) 或每週備份。

    ![Windows Server 備份項目](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > 如需有關如何 toospecify hello 備份排程的詳細資訊，請參閱 hello 文章[使用 Azure Backup tooreplace 磁帶基礎結構](backup-azure-backup-cloud-as-tape.md)。
   >
   >

8. 在 hello**選取保留原則**頁面上，選擇 hello 特定的保留原則 hello 為 hello 備份副本，然後按一下**下一步**。

    hello 保留原則指定 hello 持續時間的 hello 備份會儲存。 而不是只指定 「 一般原則 」 的所有備份的點，您可以指定不同的保留原則根據 hello 備份發生時。 您可以修改 hello 每日、 每週、 每月和每年保留原則 toomeet 您的需求。
9. 在 [hello 選擇初始備份類型] 頁面上，選擇 hello 初始備份類型。 保留 hello 選項**自動透過網路 hello**選取，然後再按一下**下一步**。

    您可以備份自動 hello 網路上或您可以離線備份。 hello 本文其餘部分說明 hello 程序會自動備份。 如果您偏好 toodo 離線備份，請檢閱 hello 文件[Azure Backup 中的離線備份工作流程](backup-azure-backup-import-export.md)如需詳細資訊。
10. 在 hello 確認頁面上，檢閱 hello 資訊，然後再按一下**完成**。
11. Hello 精靈可讓您完成建立 hello 備份排程後，按一下**關閉**。

### <a name="enable-network-throttling"></a>啟用網路節流
hello Microsoft Azure 備份代理程式會提供網路節流設定。 節流會控制資料傳輸期間的網路頻寬使用方式。 如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。 節流設定會套用 tooback 和還原活動。

> [!NOTE]
> 網路節流不適用於 Windows Server 2008 R2 SP1、Windows Server 2008 SP2 或 Windows 7 (含 service pack)。 hello Azure Backup 網路節流功能會 hello 本機作業系統上的服務品質 (QoS)。 Azure 備份可保護這些作業系統，但不適用於 Azure Backup 網路節流設定 hello QoS 適用於這些平台版本。 網路節流可使用於所有其他 [支援的作業系統](backup-azure-backup-faq.md)。
>
>

**tooenable 網路節流設定**

1. 在 hello Microsoft Azure 備份代理程式，按一下 **變更屬性**。

    ![變更屬性](./media/backup-configure-vault/change-properties.png)
2. 在 hello**節流**索引標籤，選取 hello**啟用網際網路頻寬使用節流設定的備份操作**核取方塊。

    ![網路節流](./media/backup-configure-vault/throttling-dialog.png)
3. 啟用節流設定後，指定允許的頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。

    hello 頻寬值開始每秒 (Kbps) 為 512 kb，最高 too1，023 mb / 秒 (MBps)。 也可以指定 hello 開始和完成**上班**，和 hello 一週的哪幾天都視為的工作日。 指定之工作時間以外的時間則視為非工作時間。
4. 按一下 [確定] 。

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback 檔案及資料夾的 hello 第一次
1. 在 hello 備份代理程式，按一下 **立即備份**toocomplete hello 初始植入 hello 網路上。

    ![Windows Server 立即備份](./media/backup-configure-vault/backup-now.png)
2. 在 hello 確認頁面上，檢閱 hello 立即備份精靈的 hello 設定會使用 tooback hello 機器。 然後按一下 [備份] 。
3. 按一下**關閉**tooclose hello 精靈。 如果 hello 備份程序完成之前，您可以這樣做，hello 精靈會繼續 toorun hello 背景。

Hello 初始備份完成後，hello**作業已完成**hello Backup 主控台中顯示的狀態。

![IR 已完成](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。

## <a name="next-steps"></a>後續步驟
如需備份 VM 或其他工作負載的詳細資訊，請參閱︰

* 現在您已備份好檔案和資料夾，接下來您可以 [管理您的保存庫和伺服器](backup-azure-manage-windows-server.md)。
* 如果您需要 toorestore 備份，請使用本文章太[還原檔案 tooa Windows 機器](backup-azure-restore-windows-server.md)。
