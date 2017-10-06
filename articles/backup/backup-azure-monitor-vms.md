---
title: "aaaMonitor 資源管理員部署虛擬機器備份 |Microsoft 文件"
description: "監視 Resource Manager 部署的虛擬機器備份中的事件和警示。 根據警示傳送電子郵件。"
services: backup
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: fed32015-2db2-44f8-b204-d89f6fd1bea2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: markgal;trinadhk;giridham;
ms.openlocfilehash: bf45cbaa05621b2365c26bafa1bd8223a444c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-alerts-for-azure-virtual-machine-backups"></a>監視 Azure 虛擬機器備份的警示
警示是事件閾值已達到或超過 hello 服務的回應。 了解當問題開始可以重大 tookeeping 的商務成本。 警示通常不會發生排程，並因此，很有幫助 tooknow 儘速之後便會產生警示。 例如，當備份或還原作業失敗時，發生 hello 失敗的五分鐘內的警示。 Hello 保存庫儀表板中 hello 備份警示磚會顯示重大和警告層級的事件。 在 hello 備份警示設定中，您可以檢視所有事件。 但是，如果在您處理不同問題時發生警示，您該怎麼辦？ 如果您不知道 hello 警示時，它可能是次要的不便，或它可能會危及資料。 toomake 確定 hello 正確人員了解警示-它發生時，設定透過電子郵件的 hello 服務 toosend 警示通知。 如需設定電子郵件通知的詳細資訊，請參閱 [設定通知](backup-azure-monitor-vms.md#configure-notifications)。

## <a name="how-do-i-find-information-about-hello-alerts"></a>如何找到 hello 警示的詳細資訊？
tooview 資訊有關 hello 擲回警示的事件，您必須開啟 hello 備份警示刀鋒視窗。 有兩種方式 tooopen hello 備份警示刀鋒伺服器： 從備份警示磚 hello 保存庫儀表板中的 hello 或 hello 警示與事件刀鋒視窗。

tooopen hello 備份警示刀鋒視窗，從備份警示磚：

* 在 hello**備份警示**hello 保存庫儀表板磚上，按一下 **重大**或**警告**tooview hello 操作該嚴重性層級的事件。

    ![備份警示圖格](./media/backup-azure-monitor-vms/backup-alerts-tile.png)

tooopen hello 備份警示刀鋒視窗中的 hello 警示與事件刀鋒視窗：

1. 從 hello 保存庫儀表板中，按一下 **所有設定**。 ![所有設定按鈕](./media/backup-azure-monitor-vms/all-settings-button.png)
2. 在 hello**設定**刀鋒視窗中，按一下 **警示與事件**。 ![警示和事件按鈕](./media/backup-azure-monitor-vms/alerts-and-events-button.png)
3. 在 hello**警示與事件**刀鋒視窗中，按一下 **備份警示**。 ![備份警示按鈕](./media/backup-azure-monitor-vms/backup-alerts.png)

    hello**備份警示**刀鋒視窗會開啟並顯示 hello 篩選的警示。

    ![備份警示圖格](./media/backup-azure-monitor-vms/backup-alerts-critical.png)
4. tooview 詳細的資訊有關特定警示，從 hello 清單中的事件，按一下 hello 警示 tooopen 其**詳細資料**刀鋒視窗。

    ![事件詳細資料](./media/backup-azure-monitor-vms/audit-logs-event-detail.png)

    toocustomize hello 屬性顯示在 [hello] 清單中，請參閱[檢視其他事件屬性](backup-azure-monitor-vms.md#view-additional-event-attributes)

## <a name="configure-notifications"></a>設定通知
 您可以設定 hello 服務 toosend 透過 hello 過去一小時，或發生特定類型的事件時所發生的 hello 警示的電子郵件通知。

tooset 警示的電子郵件通知

1. Hello 備份警示功能表上，按一下**設定通知**

    ![備份警示功能表](./media/backup-azure-monitor-vms/backup-alerts-menu.png)

    hello 通知設定 刀鋒視窗隨即開啟。

    ![設定通知刀鋒視窗](./media/backup-azure-monitor-vms/configure-notifications.png)
2. 在 hello 電子郵件通知，設定通知刀鋒視窗上按一下**上**。

    hello 收件者和嚴重性對話方塊具有星號的下一個 toothem，因為該資訊是必要的。 提供至少一個電子郵件地址，然後選取至少一個嚴重性。
3. 在 [hello**收件者 （電子郵件）** ] 對話方塊中，型別 hello 電子郵件地址收到 hello 通知的人員。 使用 hello 格式： username@domainname.com。用分號分 (;) 分隔多個電子郵件位址。
4. 在 hello**通知**區域中，選擇**每個警示**toosend 通知時 hello 指定警示時，或**每小時摘要**toosend hello 過去一小時的摘要。
5. 在 [hello**嚴重性**] 對話方塊中，選擇您想 tootrigger 的一或多個層級電子郵件通知。
6. 按一下 [儲存] 。

   ### <a name="what-alert-types-are-available-for-azure-iaas-vm-backup"></a>有哪些警示類型可供 Azure IaaS VM 備份使用？
   | 警示層級 | 傳送的警示 |
   | --- | --- |
   | 重要 |備份失敗、復原失敗 |
   | 警告 |None |
   | 資訊 |None |

### <a name="are-there-situations-where-email-isnt-sent-even-if-notifications-are-configured"></a>會有即使已設定通知卻不寄送電子郵件的情況嗎？
有情況下，不會傳送警示，即使已正確設定 hello 通知。 Hello 在下列情況下電子郵件不會傳送通知 tooavoid 警示的干擾：

* 如果通知設定的 tooHourly 摘要，而且會引發和解決的警示 hello 一小時內。
* hello 作業已取消。
* 備份作業會觸發然後失敗，且另一個備份作業正在進行中。
* 啟用資源管理員的 VM 的排定備份工作會啟動，但 hello VM 不存在。

## <a name="customize-your-view-of-events"></a>自訂事件的檢視
hello**稽核記錄檔**設定隨附一組預先定義的篩選和資料行顯示操作事件的相關資訊。 您可以自訂 hello 檢視，讓當 hello**事件**刀鋒視窗中開啟時，它會顯示您 hello 您想要的資訊。

1. 在 hello[保存庫儀表板](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)，瀏覽 tooand 按一下**稽核記錄檔**tooopen hello**事件**刀鋒視窗。

    ![稽核記錄檔](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    hello**事件**刀鋒視窗會開啟 toohello 操作事件篩選，只供 hello 目前保存庫。

    ![稽核記錄檔篩選器](./media/backup-azure-monitor-vms/audit-logs-filter.png)

    hello 刀鋒視窗中顯示 hello 嚴重、 錯誤、 警告和參考發生的事件中清單 hello 過去一週。 hello 時間範圍是預設值設定在 hello**篩選**。 hello**事件**刀鋒視窗也會顯示橫條圖 hello 事件發生時加以追蹤。 如果您不想 toosee hello 橫條圖中的，在 hello**事件**功能表上，按一下 **隱藏圖表**tootoggle 關閉 hello 圖表。 hello 預設檢視的事件會顯示作業、 層級、 狀態、 資源和時間資訊。 公開其他事件屬性的相關資訊，請參閱 hello 區段[展開事件資訊](backup-azure-monitor-vms.md#view-additional-event-attributes)。
2. 如需有關作業的事件，在 hello**作業**資料行中，按一下 操作事件 tooopen 其刀鋒視窗。 hello 刀鋒視窗會包含有關 hello 事件的詳細的資訊。 事件會依其相互關聯識別碼和一份 hello hello 時間範圍中發生的事件分組。

    ![Operation Details](./media/backup-azure-monitor-vms/audit-logs-details-window.png)
3. tooview 詳細的資訊關於特定事件，從 hello 清單中的事件，按一下 hello 事件 tooopen 其**詳細資料**刀鋒視窗。

    ![事件詳細資料](./media/backup-azure-monitor-vms/audit-logs-details-window-deep.png)

    hello 事件層級資訊是詳細 hello 資訊取得。 如果您想看到這麼多資訊每個事件，並希望 tooadd 這更詳細說明 toohello**事件**刀鋒視窗中，請參閱 hello 節[展開事件資訊](backup-azure-monitor-vms.md#view-additional-event-attributes)。

## <a name="customize-hello-event-filter"></a>自訂 hello 事件篩選器
使用 hello**篩選**tooadjust 或選擇特定刀鋒視窗中顯示的 hello 資訊。 toofilter hello 事件資訊：

1. 在 hello[保存庫儀表板](backup-azure-manage-vms.md#open-a-recovery-services-vault-in-the-dashboard)，瀏覽 tooand 按一下**稽核記錄檔**tooopen hello**事件**刀鋒視窗。

    ![稽核記錄檔](./media/backup-azure-monitor-vms/audit-logs-1606-1.png)

    hello**事件**刀鋒視窗會開啟 toohello 操作事件篩選，只供 hello 目前保存庫。

    ![稽核記錄檔篩選器](./media/backup-azure-monitor-vms/audit-logs-filter.png)
2. 在 hello**事件**功能表上，按一下 **篩選**tooopen 該刀鋒視窗。

    ![開放篩選刀鋒視窗](./media/backup-azure-monitor-vms/audit-logs-filter-button.png)
3. 在 hello**篩選**刀鋒視窗中，調整 hello**層級**，**時間範圍**，和**呼叫端**篩選。 hello 其他篩選器沒有因為 hello 復原服務保存庫的已設定 tooprovide hello 目前資訊。

    ![稽核記錄檔查詢詳細資料](./media/backup-azure-monitor-vms/filter-blade.png)

    您可以指定 hello**層級**的事件： 嚴重、 錯誤、 警告還是資訊。 您可以選擇任何事件層級組合，但必須選取至少一個層級。 開啟或關閉切換 hello 層級。 hello**時間範圍**篩選可讓您 toospecify hello 擷取事件的時間長度。 如果您使用自訂的時間範圍，您可以設定 hello 的開始和結束時間。
4. 當您準備好 tooquery hello 作業記錄檔使用篩選器，請按一下**更新**。 hello 結果都會顯示在 hello**事件**刀鋒視窗。

    ![Operation Details](./media/backup-azure-monitor-vms/edited-list-of-events.png)

### <a name="view-additional-event-attributes"></a>檢視其他事件屬性
使用 hello**資料行** 按鈕，您可以啟用在 hello 的 hello 清單中的其他事件屬性 tooappear**事件**刀鋒視窗。 hello 預設清單的事件顯示作業、 層級、 狀態、 資源和時間的資訊。 tooenable 額外屬性：

1. 在 hello**事件**刀鋒視窗中，按一下 **資料行**。

    ![開啟資料行](./media/backup-azure-monitor-vms/audi-logs-column-button.png)

    hello**選擇資料行**刀鋒視窗隨即開啟。

    ![資料行刀鋒視窗](./media/backup-azure-monitor-vms/columns-blade.png)
2. tooselect hello 屬性，請按一下 [hello] 核取方塊。 hello 屬性核取方塊切換開啟 / 關閉。
3. 按一下**重設**tooreset hello 份屬性清單中 hello**事件**刀鋒視窗。 在之後新增或移除屬性 hello 清單中，使用**重設**tooview hello 新的事件屬性清單。
4. 按一下**更新**tooupdate hello hello 事件屬性的資料。 hello 下表提供每個屬性的相關資訊。

| 資料行名稱 | 說明 |
| --- | --- |
| 作業 |hello hello 作業名稱 |
| Level |hello 層級 hello 作業的值可以是： 參考、 警告、 錯誤或嚴重 |
| 狀態 |描述作業狀態的 hello |
| 資源 |URL 識別 hello 資源;也稱為 hello 資源識別碼 |
| 時間 |測量從 hello hello 事件發生的目前時間的時間 |
| 呼叫者 |人員或所呼叫或觸發 hello 事件;可以是 hello 系統或使用者 |
| Timestamp |hello 事件所觸發的 hello 時間 |
| 資源群組 |hello 相關聯的資源群組 |
| 資源類型 |使用資源管理員的 hello 內部資源類型 |
| 訂用帳戶識別碼 |hello 相關聯的訂用帳戶 ID |
| 類別 |Hello 事件的類別目錄 |
| 相互關連識別碼 |相關事件的通用識別碼 |

## <a name="use-powershell-toocustomize-alerts"></a>使用 PowerShell toocustomize 警示
您可以在 hello 入口網站取得 hello 工作的自訂警示通知。 這些作業，tooget 定義 PowerShell 為基礎的警示規則上操作的 hello 記錄的事件。 使用 PowerShell 1.3.0 版或更新版本 。

toodefine 自訂通知 tooalert 備份失敗，使用下列指令碼的 hello 類似的命令：

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.RecoveryServices/recoveryServicesVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/Microsoft.RecoveryServices/vaults/trinadhVault -Actions $actionEmail
```

**ResourceId** ： 您可以取得 ResourceId hello 從稽核記錄檔。 hello ResourceId 是 hello 資源 欄中的 hello 作業記錄檔中提供的 URL。

**OperationName** : OperationName 的 hello 格式"Microsoft.RecoveryServices/recoveryServicesVault/*EventName*"其中*EventName*可以是：<br/>

* 註冊 <br/>
* Unregister  <br/>
* ConfigureProtection  <br/>
* Backup  <br/>
* Restore  <br/>
* StopProtection  <br/>
* DeleteBackupData  <br/>
* CreateProtectionPolicy  <br/>
* DeleteProtectionPolicy  <br/>
* UpdateProtectionPolicy  <br/>

**Status** ：支援的值為 [已開始]、[成功] 或 [失敗]。

**ResourceGroup** ： 這是 hello toowhich hello 資源所屬的資源群組。 您可以加入 hello 資源群組資料行 toohello 產生記錄檔。 資源群組是其中一個 hello 可用的事件資訊的類型。

**名稱**: hello 警示規則的名稱。

**CustomEmail** ： 指定您要警示的通知 toosend hello 自訂電子郵件地址 toowhich

**SendToServiceOwners** ： 這個選項會傳送警示通知 tooall 系統管理員和共同管理員的 hello 訂用帳戶。 它可以用於 **New-AzureRmAlertRuleEmail** Cmdlet 中

### <a name="limitations-on-alerts"></a>警示的限制
以事件為基礎的警示是主體 toohello 下列限制：

1. Hello 復原服務保存庫中的所有虛擬機器上便會觸發警示。 您無法自訂 hello 警示復原服務保存庫中的虛擬機器的子集。
2. 這項功能處於預覽狀態。 [深入了解](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. "alerts-noreply@mail.windowsazure.com" 會傳送警示。 目前您無法修改 hello 電子郵件寄件者。

## <a name="next-steps"></a>後續步驟
事件記錄檔啟用絕佳事後和稽核 hello 備份作業的支援。 記錄 hello 下列作業：

* 註冊
* Unregister 
* 設定保護
* 備份 (排程和隨選備份兩者)
* Restore 
* 停止保護
* 刪除備份資料
* Add policy
* 刪除原則
* 更新原則
* 取消工作

如需事件、 作業和跨 hello 的稽核記錄檔的廣泛說明 Azure 服務，請參閱 hello 文章[檢視的事件，並稽核記錄檔](../monitoring-and-diagnostics/insights-debugging-with-events.md)。

如需從復原點重新建立虛擬機器的詳細資訊，請參閱 [還原 Azure VM](backup-azure-restore-vms.md)。 如果您需要保護虛擬機器的詳細資訊，請參閱[第一印象： 備份復原服務保存庫的 Vm tooa](backup-azure-vms-first-look-arm.md)。 深入了解 hello hello 文章中的 VM 備份的管理工作[管理 Azure 虛擬機器備份](backup-azure-manage-vms.md)。
