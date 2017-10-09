---
title: "Azure 備份伺服器 v2 aaaInstall |Microsoft 文件"
description: "Azure 備份伺服器 v2 可提供您經過強化的備份功能，讓您保護 VM、檔案和資料夾以及工作負載等項目。 深入了解如何 tooinstall 或升級 tooAzure 備份伺服器 v2。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>安裝 Azure 備份伺服器 v2

Azure 備份伺服器可協助保護您的虛擬機器 (VM)、工作負載以及檔案和資料夾等項目。 Azure 備份伺服器 v2 是以 Azure 備份伺服器 v1 作為建置基礎，並可提供您 v1 所沒有的新功能。 如需 v1 和 v2 的功能比較，請參閱 [Azure 備份伺服器保護對照表](backup-mabs-protection-matrix.md)。 

hello 備份伺服器 v2 中的其他功能，包括備份伺服器 v1 升級。 不過，並非一定要有備份伺服器 v1 才能安裝備份伺服器 v2。 如果您要從備份伺服器 v1 tooBackup 伺服器 v2 tooupgrade，安裝備份伺服器 v2 hello 備份伺服器保護伺服器上。 您現有的備份伺服器設定會保持不變。

您可以在 Windows Server 2012 R2 或 Windows Server 2016 上安裝備份伺服器 v2。 tootake 使用新的功能類似 System Center 2016 的資料保護管理員現代化備份存放裝置，您必須安裝 Windows Server 2016 上的備份伺服器 v2。 升級 tooor 安裝 v2 備份伺服器之前，請閱讀 hello[安裝必要條件](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)。

> [!NOTE]
> Azure 備份伺服器具有 hello 相同程式碼基底為 System Center Data Protection Manager。 備份伺服器 v1 相等 tooData Protection Manager 2012 R2 中，並備份伺服器 v2 是對等 tooData Protection Manager 2016。 這篇文章偶爾會參考 hello Data Protection Manager 文件。
>
>

## <a name="upgrade-backup-server-toov2"></a>升級備份伺服器 toov2
從備份伺服器 v1 tooBackup 伺服器 v2 tooupgrade 請確定您的安裝具有所需的 hello 更新：

- [Hello 保護代理程式更新](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent)hello 上受保護的伺服器。
- 升級 Windows Server 2012 R2 tooWindows Server 2016。
- 在所有生產伺服器上升級 Azure 備份伺服器遠端系統管理員。
- 確定備份設定 toocontinue 不需要重新啟動您的實際伺服器。


### <a name="upgrade-steps-for-backup-server-v2"></a>備份伺服器 v2 的升級步驟

1. 在 hello Download Center[下載 hello 升級安裝程式](https://go.microsoft.com/fwlink/?LinkId=626082)。

2. 擷取 hello 安裝精靈之後，請確定**執行 setup.exe**已選取，然後選取**完成**。

  ![設定安裝程式 - 執行設定](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. 在 hello Microsoft Azure 備份伺服器精靈 在**安裝**，選取**Microsoft Azure 備份伺服器**。

  ![設定安裝程式 - 選取安裝](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. 在 hello ** 褖畫惎**頁面上，檢閱 hello 警告，然後選取**下一步**。

  ![設定安裝程式 - [歡迎使用] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. hello 安裝精靈會執行必要條件檢查 toomake 確定可以升級您的環境。 在 hello **Prerequisite Checks**頁面上，選取**檢查**。

  ![設定安裝程式 - [必要條件檢查] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. 您的環境必須通過 hello 必要條件檢查。 如果您的環境未通過 hello 檢查，請注意 hello 問題並加以修正。 然後，選取 [再檢查一次]。 您傳遞 hello 必要條件檢查之後，請選取**下一步**。

  ![設定安裝程式 - [再檢查一次] 按鈕](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. 在 hello **SQL 設定**頁面上，選取您的 SQL 安裝的 hello 相關選項，然後選取**檢查並安裝**。

  ![設定安裝程式 - [SQL 設定] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  hello 檢查可能需要幾分鐘的時間。 當 hello 檢查是否已完成，請選取**下一步**。

  ![設定安裝程式 - [SQL 設定] 的 [檢查並安裝] 按鈕](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. 在 hello**安裝設定**頁面上，進行備份伺服器安裝所在的任何變更 toohello 位置或 toohello 可用位置。 選取 [下一步] 。

  ![設定安裝程式 - [安裝設定] 頁面](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello 安裝精靈中，選取**完成**。

  ![設定安裝程式 - 完成](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>為新式備份儲存體新增儲存體

tooimprove 備份儲存體效率，備份伺服器 v2 加入磁碟區的支援。 和備份伺服器 v1 一樣，備份伺服器 v2 也支援磁碟。

### <a name="add-volumes-and-disks"></a>新增磁碟區和磁碟
如果您在 Windows Server 2016 上執行備份伺服器 v2，您可以使用磁碟區 toostore 備份資料。 磁碟區可節省儲存空間並提高備份速度。 因為磁碟區是新 tooBackup 伺服器，您必須將其加入。 

當您新增的磁碟區 tooBackup 伺服器時，您可以提供 hello 磁碟區的好記名稱。 按一下 hello**易記名稱**資料行要 tooname 的 hello 磁碟區。 如有必要，您可以稍後變更 hello 名稱。 您也可以使用 PowerShell tooadd 或變更磁碟區的好記名稱。

tooadd hello 系統管理員主控台中的磁碟區：

1. 在 hello Azure 備份伺服器系統管理員主控台中，選取 **管理** > **磁碟儲存體** > **新增**。

    ![開啟 hello 加入磁碟儲存體精靈](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    這會開啟 hello 加入磁碟儲存體精靈。

2. 在 hello**加入磁碟儲存體**] 頁面的 hello**可用的磁碟區**，選取 [磁碟區，然後選取**新增**。
3. 在 hello**選取磁碟區**方塊、 輸入 hello 磁碟區的好記名稱，然後選取**確定**。

      ![新增磁碟儲存體精靈 - 新增磁碟區](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  如果您想 tooadd 磁碟，hello 磁碟必須屬於 tooa 保護群組具有傳統存放裝置。 這些磁碟僅能用於這些保護群組。 備份伺服器並沒有有舊版保護的來源，如果未列出 hello 磁碟。

  如需新增磁碟的詳細資訊，請參閱[新增磁碟 tooincrease 傳統儲存體](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage)。 您不能對磁碟賦予易記名稱。


### <a name="assign-workloads-toovolumes"></a>指定工作負載 toovolumes

備份伺服器，在您指定的工作負載指派 toowhich 磁碟區。 例如，您可以設定昂貴支援大量輸入/輸出作業每個第二個 (IOPS) toostore 唯一需要的工作負載高容量頻繁備份的磁碟區。 舉例來說，具有交易記錄的 SQL Server。

#### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

備份伺服器 hello 存放集區中的磁碟區 tooupdate hello 屬性，請使用 PowerShell 指令程式更新 DPMDiskStorage hello。

語法：

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

使用 PowerShell 進行的所有變更會都反映在 hello UI。


## <a name="protect-data-sources"></a>保護資料來源
toobegin 保護資料來源，建立保護群組。 hello 遵循步驟反白顯示變更或新增 toohello 新保護群組精靈。

toocreate 保護群組：

1. 在 hello 備份伺服器系統管理員主控台中，選取 **保護**。

2. 在 hello 工具功能區中，選取 **新增**。

    這會開啟 hello 建立新保護群組精靈。

  ![建立新保護群組精靈](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. 在 hello ** 褖畫惎**頁面上，選取**下一步**。
4. 在 hello**選取保護群組類型**頁面上，選取您想 toocreate，，然後選取保護群組的 hello 類型**下一步**。

  ![[選取保護群組類型] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. 在 hello**選擇群組成員** 頁面的 hello**可用成員**窗格中，保護代理程式會列出與 hello 成員。 針對此範例中，選取 磁碟區 D:\ 和 E:\ 並將其新增 toohello**選取的成員**窗格。 選取 [下一步] 。

  ![[選取群組成員] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. 在 [hello**選擇資料保護方式**頁面上，輸入**保護群組名稱**選取 hello 保護方式，，然後選取**下一步]**。 如果您想要短期保護，您必須選取 hello**磁碟**備份方法。

  ![[選取資料保護方式] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. 在 hello**指定短期目標**頁面上，選取 hello 詳細資料**保留範圍**和**同步處理頻率**。 然後，選取 [下一步]。 （選擇性） toochange hello 排程復原點時所建立，請選取**修改**。

  ![[指定短期目標] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. 在 hello**檢閱磁碟儲存體配置**頁面檢閱有關 hello 您選取的資料來源的詳細資料、 大小和 hello 空間 toobe 佈建的值，並 hello 目標儲存體磁碟區。

  ![[檢閱磁碟儲存體配置] 頁面](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  存放磁碟區依據 hello （使用 PowerShell 設定） 的工作負載磁碟區配置和 hello 可用的存放裝置。 您可以變更 hello 存放磁碟區 hello 下拉式選單中選取其他磁碟區。 如果您變更 hello 值**目標儲存體**，hello 值**可用的磁碟儲存體**tooreflect 值底下會動態變更**可用空間**和**Underprovisioned 空間**。

  Hello 資料來源成長為已規劃，hello 值 hello **Underprovisioned 空間**中的資料行**可用的磁碟儲存體**反映 hello 額外的存放裝置所需的數量。 使用您的儲存體需要 smooth 備份此值 toohelp 計劃。 Hello 值為零中, 有任何儲存體可能造成的問題 hello 可預見未來。 Hello 值為非零的數字，如果您沒有足夠的儲存空間配置 （根據您保護原則 hello 資料大小和受保護的成員）。

  ![配置不足的磁碟儲存體](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   建立保護群組、 完整 hello 精靈 toofinish。

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>移轉舊版的儲存體 tooModern 備份儲存體
Tooor 安裝備份伺服器 v2 和升級 hello 作業系統 tooWindows Server 2016 的升級之後，更新您的保護群組 toouse 現代的備份儲存體。 根據預設，系統不會變更保護群組。 他們可以繼續 toofunction 它們一開始所設定。 

更新保護群組 toouse 現代的備份儲存體是選擇性的。 tooupdate hello 保護群組時，使用 hello 的所有資料來源停止保護保留資料選項。 然後，加入 hello 資料來源 tooa 新的保護群組。

1. 在 hello 系統管理員主控台中，選取 hello**保護**功能。 在 hello**保護群組成員**清單中，以滑鼠右鍵按一下 hello 成員，然後選取**停止保護成員**。

  ![停止保護成員](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. 在 [hello**從群組移除**] 對話方塊中，檢閱 hello 使用磁碟空間和 hello 可用空間 hello 存放集區。 hello 預設值為 hello 磁碟上的 tooleave hello 復原點，而且允許這些 tooexpire 每個關聯的保留原則。 按一下 [確定] 。

  如果您想 tooimmediately 傳回 hello 使用磁碟空間 toohello 可用儲存集區，選取 hello**刪除磁碟上的複本**與成員相關的核取方塊 toodelete hello 備份資料 （和復原點）。

  ![[從群組中移除] 對話方塊](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. 建立使用新式備份儲存體的保護群組。 包含 hello 未受保護資料來源。


## <a name="add-disks-tooincrease-legacy-storage"></a>新增磁碟 tooincrease 傳統存放裝置

如果您想 toouse 傳統存放裝置，且備份伺服器，您可能需要 tooadd 磁碟 tooincrease 傳統儲存體。 

tooadd 磁碟儲存體：

1. 在 hello 系統管理員主控台中，選取 **管理** > **磁碟儲存體** > **新增**。

    ![[新增磁碟儲存體] 對話方塊](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. 在 hello**加入磁碟儲存體**對話方塊中，選取**新增磁碟**。

5. Hello 在清單中可用的磁碟，請選取您想要選取 tooadd 的 hello 磁碟**新增**，然後選取**確定**。

## <a name="update-hello-data-protection-manager-protection-agent"></a>更新 hello Data Protection Manager 保護代理程式

備份伺服器使用 hello System Center Data Protection Manager 保護代理程式更新。 如果您要升級保護代理程式未連接的 toohello 網路，您無法使用 hello 資料保護 Manager 系統管理員主控台 toocomplete 連接的代理程式升級。 您必須先升級非作用中網域環境中的 hello 保護代理程式。 連接的 toohello 網路 hello 用戶端電腦之前，資料保護 Manager 系統管理員主控台會顯示該 hello 保護代理程式更新的 hello 已暫止。

hello 下列各節說明如何 tooupdate 連線的用戶端電腦和未連接的用戶端電腦的保護代理程式。

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>更新已連線用戶端電腦的保護代理程式

1. 在 hello 備份伺服器系統管理員主控台中，選取 **管理** > **代理程式**。

2. Hello 顯示窗格中，選取您要為其 tooupdate hello 保護代理程式的 hello 用戶端電腦。

  > [!NOTE]
  > hello**代理程式更新**欄位指出當保護代理程式更新為適用於每個受保護的電腦。 在 hello**動作**窗格中，hello**更新**動作可用，只會選取受保護的電腦，並更新可供使用。
  >
  >

3. tooinstall 更新保護代理程式選取 hello 在電腦上，在 hello**動作**窗格中，選取**更新**。

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>在未連線用戶端電腦上更新保護代理程式

1. 在 hello 備份伺服器系統管理員主控台中，選取 **管理** > **代理程式**。

2. Hello 顯示窗格中，選取您要為其 tooupdate hello 保護代理程式的 hello 用戶端電腦。

  > [!NOTE]
   > hello**代理程式更新**欄位指出當保護代理程式更新為適用於每個受保護的電腦。 在 hello**動作**窗格中，hello**更新**動作時，無法使用選取的受保護的電腦，除非有可用的更新。
  >
  >

3. tooinstall 更新保護代理程式選取 hello 在電腦上，選取**更新**。

4. Hello 電腦是連線的 toohello 網路之前，不是用戶端電腦已連接 toohello 網路，hello**代理程式狀態**資料行會顯示狀態為**更新擱置**。

  用戶端電腦是連線的 toohello 網路之後，hello**代理程式更新**hello 用戶端電腦的資料行會顯示狀態為**更新**。
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>移動從舊的版本，以及與 Azure 同步 hello 新版本的舊版保護群組

一旦 Azure 備份伺服器和 hello 作業系統會同時更新，您就準備好 tooprotect 新的資料來源使用現代的備份儲存體。 不過已受保護的資料來源將會繼續 toobe hello 舊版中受保護的方式與 Azure 備份伺服器 中，但是所有新的保護將會使用現代的備份存放裝置。

下列步驟是 toomigrate 資料來源從保護 tooModern 備份儲存體的傳統模式。

• 新增 hello 新磁碟區 toohello DPM 存放集區，並視需要指派易記名稱和資料來源的標記。
• 在舊版模式下，停止保護 hello 資料來源和 「 保留受保護的資料 」 的每個資料來源。  這允許在移轉之後復原舊的復原點。

• 建立新的 PG，然後選取 hello toobe 使用新格式儲存的資料來源。
• DPM 將執行從 hello 舊版備份儲存體複本複製到 hello 本機現代的備份存放磁碟區。
注意：這會被視為復原後作業 • 所有新的同步處理和復原點則會儲存在新式備份儲存體中。
將出剪除 • 舊的復原點，視為過期，而且最後釋出 hello 磁碟空間。
• 從 hello 舊的存放裝置 hello 磁碟中刪除所有與 hello 傳統的磁碟區之後可以從 Azure 的備份與 hello 系統中移除。
• 進行 hello Azure DPMDB 的備份。

第 2 部分:-重要的項目 > hello 新伺服器將需要 toobe 為 hello 原始的 Azure 備份伺服器名稱相同。 如果您想 toouse 舊的存放集區和 DPMDB tooretain 復原點-必須有 DPMDB 備份，因為它必須 toobe 還原，您無法變更 hello hello 新的 Azure 備份伺服器名稱

1) 關機 hello 原始的 Azure 備份伺服器，或起飛 hello 網路。
2) 重設 active directory 中的 hello 機器帳戶。
3) 安裝 Server 2016 新電腦上以及其 hello hello 原始的 Azure 備份伺服器機器名稱相同的名稱。
4) 加入 hello 網域
5) 安裝 Azure 備份伺服器 V2 (從舊伺服器中移出 DPM 儲存集區並匯入)
6) 還原取自第 2 部分結束 DPMDB hello
7) 將 hello 存放裝置連接從 hello 原始備份伺服器 toohello 新伺服器。
8) 從 SQL 還原 hello DPMDB
9) 新的伺服器 cd tooMicrosoft Azure 備份的系統管理員命令列安裝位置和 bin 資料夾

路徑範例：C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
tooAzure 備份執行 DPMSYNC-SYNC

10) 執行 DPMSYNC-SYNC 附註如果加入了新磁碟 toohello DPM 存放集區而不需要移動 hello 舊的然後執行 DPMSYNC-Reallocatereplica

## <a name="new-powershell-cmdlets-in-v2"></a>v2 中的新 PowerShell Cmdlet

當您在安裝 Azure 備份伺服器 v2 時，系統有兩個新的 Cmdlet 可供使用： 
* [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>後續步驟

深入了解如何 tooprepare 您的伺服器或開始進行保護工作負載：
- [準備備份伺服器工作負載](backup-azure-microsoft-azure-backup.md)
- [使用 VMware 伺服器的備份伺服器 tooback](backup-azure-backup-server-vmware.md)
- [使用 SQL server 備份伺服器 tooback](backup-azure-sql-mabs.md)
- [在備份伺服器中使用新式備份儲存體](backup-mabs-add-storage.md)

