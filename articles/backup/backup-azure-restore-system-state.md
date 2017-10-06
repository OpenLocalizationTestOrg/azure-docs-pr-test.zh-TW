---
title: "Azure 備份： Windows Server 還原系統狀態 tooa |Microsoft 文件"
description: "如何從 Azure 中的備份來還原 Windows Server 系統狀態的逐步解說。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>還原系統狀態 tooWindows 伺服器

本文說明如何從 Azure 復原服務 toorestore Windows 伺服器系統狀態備份保存庫。 toorestore 系統狀態，您必須有系統狀態備份 (使用中的 hello 指示建立[備份系統狀態](backup-azure-system-state.md#back-up-windows-server-system-state-preview))，並確定您已安裝 hello[最新版本的 Microsoft Azure Recovery hello服務 (MARS) 代理程式](http://aka.ms/azurebackup_agent)。 從 Azure 復原服務保存庫來復原 Windows Server 系統狀態資料的程序需要兩個步驟：

1. 從 Azure 備份來還原檔案形式的系統狀態。 在從 Azure 備份來還原檔案形式的系統狀態時，您可以：
  * 還原系統狀態 toohello 相同的伺服器，其中 hello 備份在進行，或
  * 還原系統狀態檔案 tooan 替代伺服器。

2. 適用於 hello 還原系統狀態檔案 tooa Windows 伺服器。


## <a name="recover-system-state-files-toohello-same-server"></a>復原系統狀態檔案 toohello 相同的伺服器
hello 下列步驟說明如何 tooroll 回您 Windows Server 設定 tooa 先前的狀態。 復原您的伺服器設定後 tooa 已知，穩定的狀態，可以是非常重要。 hello 復原服務保存庫中的下列步驟還原 hello 伺服器的系統狀態。 

1. 開啟 hello **Microsoft Azure 備份**嵌入式管理單元。 如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Microsoft Azure 備份**。

    hello 桌面應用程式應該會出現在 hello 搜尋結果中。

2. 按一下**復原資料**toostart hello 精靈。

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. Hello 上**入門**窗格中，toorestore hello 資料 toohello 相同伺服器或電腦上，選取**這部伺服器 (`<server name>`)**按一下**下一步**。

    ![選擇此伺服器選項 toorestore hello 資料 toohello 同一部電腦](./media/backup-azure-restore-system-state/samemachine.png)

4. 在 [hello**選取復原模式**] 窗格中，選擇**系統狀態**，然後按一下**下一步**。

    ![瀏覽檔案](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. 中的 hello 行事曆上**選取磁碟區和日期**窗格中，選取復原點。 

    您可以從任何時間的復原點還原。 日期**粗體**表示 hello 至少一個復原點的可用性。 一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。

    ![磁碟區和日期](./media/backup-azure-restore-system-state/select-date.png)

6. 一旦您已選擇 hello 復原點 toorestore，按一下 **下一步**。

    Azure 備份掛接 hello 本機復原點，並使用它做為復原磁碟區。

7. 在 hello 下一步 窗格中，指定 hello 的 hello 目的地復原系統狀態檔案，然後按一下**瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。 hello 選項，**建立複本，以擁有兩個版本**，而不是建立 hello 副本 hello 整個系統的狀態保存現有系統狀態檔案封存中建立個別的檔案複製。

    ![修復選項](./media/backup-azure-restore-system-state/recover-as-files.png)

8. 請確認 hello 詳細資料的復原在 hello**確認**按一下**復原**。

   ![按一下 復原 tooacknowledge hello 復原動作](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. 複製 hello *WindowsImageBackup*目錄 hello 復原目的地 tooa 非重要磁碟區的 hello 伺服器中。 通常，hello Windows 作業系統磁碟區是 hello 重要磁碟區。

10. Hello 復原成功之後，請遵循 hello 區段中的 hello 步驟[套用還原系統狀態檔案 toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server)，toocomplete hello 系統狀態復原程序。

## <a name="recover-system-state-files-tooan-alternate-server"></a>復原系統狀態檔案 tooan 替代伺服器

如果您的 Windows 伺服器已損毀或無法存取，而且您想 toorestore 它 tooa 穩定的狀態復原 hello Windows 伺服器系統狀態，您可以從另一部伺服器還原 hello 損毀的伺服器的系統狀態。 使用下列步驟 toohello 還原系統狀態不同的伺服器上的 hello。  

包含下列步驟中所使用的 hello 術語：

- *來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。
- *目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。
- *範例保存庫*– hello 復原服務保存庫 toowhich hello*來源機器*和*目標機器*註冊。 <br/>

> [!NOTE]
> 從一部電腦的備份無法還原的 tooa 執行舊版的 hello 作業系統的電腦。 比方說，Windows Server 2016 機器不能從備份還原 tooWindows Server 2012 R2。 然而，反向 hello 有可能。 您可以使用從 Windows Server 2012 R2 toorestore Windows Server 2016 的備份。
>

1. 開啟 hello **Microsoft Azure 備份**嵌入式管理單元在 hello*目標機器*。
2. 請確定該 hello*目標機器*和 hello*來源機器*是相同的復原服務保存庫註冊的 toohello。
3. 按一下**復原資料**tooinitiate hello 工作流程。

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)

4. 選取 [其他伺服器] 

    ![其他伺服器](./media/backup-azure-restore-system-state/anotherserver.png)

5. 提供對應 toohello hello 保存庫認證檔案*範例保存庫*。 如果 hello 保存庫認證檔案無效 （或已過期），下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 入口網站中。 一旦提供 hello 保存庫認證檔案，則會出現 hello 與 hello 保存庫認證檔案相關聯的復原服務保存庫。

6. 在 hello 選取備份伺服器 窗格中，選取 hello*來源機器*從 hello 顯示的電腦清單。

    ![電腦清單](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. 在 hello 選取復原模式 窗格中，選擇 **系統狀態**按一下**下一步**。 

    ![搜尋](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. 在 hello hello 行事曆上**選取磁碟區和日期**窗格中，選取復原點。 您可以從任何時間的復原點還原。 日期**粗體**表示 hello 至少一個復原點的可用性。 一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。 

    ![搜尋項目](./media/backup-azure-restore-system-state/select-date.png)

9. 一旦您已選擇 hello 復原點 toorestore，按一下 **下一步**。

10. 在 hello**選取系統狀態復原模式** 窗格中，指定您想執行系統狀態檔案的復原，toobe hello 目的地，然後按一下 **下一步**。

    ![加密](./media/backup-azure-restore-system-state/recover-as-files.png)

    hello 選項，**建立複本，以擁有兩個版本**，而不是建立 hello 副本 hello 整個系統的狀態保存現有系統狀態檔案封存中建立個別的檔案複製。

11. 確認 hello 詳細資料的復原在 hello 確認窗格中，然後按一下 **復原**。 

    ![按一下 hello 復原按鈕 tooconfirm hello 復原程序](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. 複製 hello *WindowsImageBackup*目錄 tooa 非重要磁碟區的 hello 伺服器 (例如 d:\)。 通常 hello Windows 作業系統磁碟區是 hello 重要磁碟區。

13. toocomplete hello 復原程序，使用 hello 下列區段太[適用於 Windows Server 上的 hello 還原系統狀態檔案](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server)。




## <a name="apply-restored-system-state-on-a-windows-server"></a>將還原的系統狀態套用到 Windows Server 上

一旦您已經復原系統狀態，以使用 Azure 復原服務代理程式的檔案，使用 hello Windows Server Backup 公用程式 tooapply hello 復原系統狀態 tooWindows 伺服器。 hello Windows Server Backup 公用程式已有 hello 伺服器上。 hello 下列步驟說明如何 tooapply hello 復原系統狀態。

1. 使用 hello 下列命令 tooreboot 伺服器*目錄服務修復模式*。 在提高權限的命令提示字元上：

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Hello 重新開機後，開啟 hello Windows Server Backup 嵌入式管理單元。 如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Windows Server Backup**。

    hello 桌面應用程式會出現在 hello 搜尋結果。

3. 在 [hello] 嵌入式管理單元，選取**本機備份**。

    ![從該處選取 本機備份 toorestore](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Hello 本機備份在主控台上，在 hello**動作 窗格**，按一下 **復原**tooopen hello 復原精靈。

5. 選取 hello 選項**儲存在另一個位置的備份**，然後按一下**下一步**。

   ![選擇 toorecover tooa 不同的伺服器](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. 指定 hello 位置類型，請選取**遠端共用資料夾**如果您的系統狀態備份復原的 tooanother 伺服器。 如果您在本機復原系統狀態，則請選取 [本機磁碟機]。 

    ![選取是否從本機伺服器或另一個 toorecovery](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. 輸入 hello 路徑 toohello *WindowsImageBackup*目錄，或選擇包含使用 「 Azure 復原 hello 系統狀態檔案復原過程復原此目錄 (例如，D:\WindowsImageBackup) hello 本機磁碟機服務代理程式和按一下**下一步**。

    ![路徑 toohello 共用的檔案](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. 選取 hello 系統狀態版本，您想 toorestore，然後按一下 **下一步**。

9. 在 hello 選取復原類型 窗格中，選取 **系統狀態**按一下**下一步**。

10. Hello 的 hello 系統狀態復原的位置，請選取**原始位置**，然後按一下**下一步**。

11. 檢閱 hello 確認詳細資料，請檢查 hello 重新開機設定，然後按一下**復原**tooapplly hello 還原系統狀態檔案。

    ![啟動 hello 還原系統狀態檔案](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>在 Active Directory 伺服器上復原系統狀態的特殊考量

系統狀態備份中包含了 Active Directory 資料。 使用下列步驟 toorestore Active Directory 網域服務 (AD DS) 從目前的狀態 tooa 先前狀態的 hello。

1. 重新啟動 hello 網域控制站在目錄服務還原模式 (DSRM)。
2. 請依照下列步驟 hello[這裡](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx)toouse Windows Server Backup cmdlet toorecover AD DS。


## <a name="troubleshoot-failed-system-state-restore"></a>針對失敗的系統狀態還原進行疑難排解

Hello 套用系統狀態的上一個程序未成功完成時，如果使用 Windows Server hello Windows 修復環境 (Win RE) toorecover。 hello 下列步驟說明如何使用 Win RE toorecover。 請在 Windows Server 不會於系統狀態還原後正常開機時，才使用此選項。 hello 程序之後清除非系統資料，請留意。 

1. 您的 Windows 伺服器開機進入 Windows 修復環境 (Win RE) hello。

2. 選取從 hello 三個可用選項的疑難排解。

    ![開啟功能表](./media/backup-azure-restore-system-state/winre-1.png)

3. 從 hello**進階選項**畫面上，選取**命令提示字元**提供 hello 伺服器系統管理員使用者名稱和密碼。

   ![開啟功能表](./media/backup-azure-restore-system-state/winre-2.png)

4. 提供 hello 伺服器系統管理員使用者名稱和密碼。

    ![開啟功能表](./media/backup-azure-restore-system-state/winre-3.png)

5. 當您以系統管理員模式開啟 hello 命令提示字元時，執行下列命令 tooget hello 系統狀態備份版本。

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-4.png)

6. 執行下列命令 tooget hello hello 備份中可用的所有磁碟區。

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-5.png)

7. hello 下列命令會復原所有磁碟區屬於 hello 系統狀態備份。 請注意此步驟中復原只 hello 重要磁碟區屬於 hello 系統狀態。 非系統資料全都會遭到清除。

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>後續步驟
* 現在您已復原檔案和資料夾，接下來您可以 [管理您的備份](backup-azure-manage-windows-server.md)。
