---
title: "aaaManage 和監視 Azure 虛擬機器備份 |Microsoft 文件"
description: "了解如何 toomanage 和監視 Azure 虛擬機器的備份"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>管理一般的 Azure 備份作業與 hello 傳統入口網站中的觸發程序警示
> [!div class="op_single_selector"]
> * [管理 Azure VM 備份](backup-azure-manage-vms.md)
> * [管理傳統 VM 備份](backup-azure-manage-vms-classic.md)
>
>

本文針對 Azure 中受保護的傳統模型虛擬機器，提供一般管理和監視工作的相關資訊。  

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 請參閱[準備 Azure 虛擬機器註冊您的環境 tooback](backup-azure-vms-prepare.md)如需詳細資訊，使用傳統部署模型的 Vm。
>
> [!IMPORTANT]
>從開始 2017 年 3 月，您無法再使用 hello 傳統入口網站 toocreate 備份保存庫。
>
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。

## <a name="manage-protected-virtual-machines"></a>管理受保護的虛擬機器
toomanage 受保護的虛擬機器：

1. tooview 及管理備份設定，如虛擬機器按一下 [hello**受保護項目**] 索引標籤。
2. 按一下 受保護項目的 toosee hello hello 名稱**備份詳細資料**索引標籤上，它會顯示 hello 上次備份的相關資訊。

    ![虛擬機器備份](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview 和管理備份原則設定，如虛擬機器按一下 [hello**原則**] 索引標籤。

    ![虛擬機器原則](./media/backup-azure-manage-vms/manage-policy-settings.png)

    hello**備份原則**索引標籤上顯示 hello 現有的原則。 您可以視需要修改。 如果您需要新的原則 toocreate 按一下**建立**上 hello**原則**頁面。 請注意，如果您想 tooremove 原則它不應該與它相關聯的任何虛擬機器。

    ![虛擬機器原則](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. 取得 hello 上的虛擬機器的動作或狀態的相關資訊**作業**頁面。 更多詳細資料或篩選的工作特定的虛擬機器，請按一下 hello 清單 tooget 中的工作。

    ![工作](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>虛擬機器的隨選備份
設定保護後，您可以執行虛擬機器的隨選備份。 如果暫止 hello 初始備份 hello 虛擬機器，隨備份將會在 Azure 備份保存庫中建立 hello 虛擬機器的完整複本。 如果第一次備份完成時，備份將會隨僅傳送變更，從上一次備份 tooAzure 備份保存庫也就是它一律為增量。

> [!NOTE]
> 視備份的保留範圍設定為指定的備份原則對應 toohello VM 中的每日保留期 tooretention 值。  
>
>

虛擬機器的 tootake 隨備份：

1. 瀏覽 toohello**受保護項目**頁面，然後選取**Azure 虛擬機器**為**類型**（如果尚未選取），然後按一下 [**選取**] 按鈕。

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. 選取 hello 虛擬機器的方法，您可以想 tootake 隨備份，然後按一下**立即備份**在 hello hello 頁面底部的按鈕。

    ![立即備份](./media/backup-azure-manage-vms/backup-now.png)

    這會在 hello 選取虛擬機器上建立備份作業。 透過這項作業所建立的復原點的保留範圍將會與 hello hello 虛擬機器相關聯的原則中指定相同的。

    ![建立備份作業](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > tooview hello 原則相關聯的虛擬機器，向下切入向下 hello 中的虛擬機器到**受保護項目**頁面和移 toobackup 原則 索引標籤。
   >
   >
3. Hello 工作建立之後，您可以按一下**檢視工作**中列 toosee hello 相對應的工作 hello 作業 頁面中的 hello 快顯的按鈕。

    ![建立的備份作業](./media/backup-azure-manage-vms/created-job.png)
4. Hello 工作順利完成之後, 建立復原點將會是您可以使用 toorestore hello 虛擬機器。 這也會增加 hello 復原點的資料行值中的 1**受保護項目**頁面。

## <a name="stop-protecting-virtual-machines"></a>停止保護虛擬機器
您可以選擇 toostop hello 未來備份的虛擬機器，以 hello 下列選項：

* 保留 Azure 備份保存庫中與虛擬機器相關聯的備份資料
* 刪除與虛擬機器相關聯的備份資料

如果您已經選取 tooretain 備份虛擬機器相關聯的資料，您可以使用 hello 備份資料 toorestore hello 虛擬機器。 如需這類虛擬機器的定價詳細資訊，請按一下 [這裡](https://azure.microsoft.com/pricing/details/backup/)。

tooStop 虛擬機器的保護：

1. 瀏覽過**受保護項目**頁面，然後選取**Azure 虛擬機器**當做 hello 篩選類型 （如果尚未選取），並按一下**選取** 按鈕。

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. 選取 hello 虛擬機器，然後按一下 **停止保護**hello hello 頁底端。

    ![停止保護](./media/backup-azure-manage-vms/stop-protection.png)
3. 根據預設，Azure Backup 不會刪除 hello hello 虛擬機器相關聯的備份資料。

    ![確認停止保護](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    如果您想 toodelete 備份資料，請選取 [hello] 核取方塊。

    ![核取方塊](./media/backup-azure-manage-vms/checkbox.png)

    請選擇停止 hello 備份的原因。 雖然這是選擇性的則提供原因將會協助 Azure Backup toowork hello 的意見反應並優先處理 hello 客戶案例。
4. 按一下**送出**按鈕 toosubmit hello**停止保護**作業。 按一下**檢視工作**toosee hello 中相對應的 hello 工作**作業**頁面。

    ![停止保護](./media/backup-azure-manage-vms/stop-protect-success.png)

    如果您沒有選取**刪除相關聯的備份資料**選項期間**停止保護**精靈，然後 post 作業完成時，保護狀態會變更太**停止保護**. hello 資料維持向 Azure 備份，直到明確刪除。 您隨時都可以刪除 hello 資料選取 hello 虛擬機器在 hello**受保護項目**頁面，然後按一下**刪除**。

    ![已停止保護](./media/backup-azure-manage-vms/protection-stopped-status.png)

    如果您已選取 hello**刪除相關聯的備份資料**選項，hello 虛擬機器將不會屬於 hello**受保護項目**頁面。

## <a name="re-protect-virtual-machine"></a>重新保護虛擬機器
如果您沒有選取 hello**刪除關聯的備份資料**選項**停止保護**，之後，您可以重新保護 hello 虛擬機器組成 hello 步驟類似 toobacking 註冊虛擬機器。 受保護，此虛擬機器會具有保留的備份資料先前 toostop 保護並且之後建立復原點之後重新保護。

之後再重新執行保護，hello 虛擬機器的保護狀態就會變更太**保護**如果太前一個復原點**停止保護**。

  ![重新保護的 VM](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> 當重新保護 hello 虛擬機器時，您可以選擇不同的原則，小於 hello 原則與虛擬機器已受保護一開始。
>
>

## <a name="unregister-virtual-machines"></a>取消註冊虛擬機器
若要從備份保存庫 hello tooremove hello 虛擬機器：

1. 按一下 hello**取消註冊**在 hello hello 頁面底部的按鈕。

    ![停用保護](./media/backup-azure-manage-vms/unregister-button.png)

    快顯通知會出現在 hello 要求確認囉 」 畫面底部。 按一下**是**toocontinue。

    ![停用保護](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>刪除備份資料
您可以刪除 hello 與虛擬機器，可能是相關聯的備份資料：

* 在停止保護作業期間
* 在虛擬機器上完成停止保護作業之後

toodelete hello 中的虛擬機器的備份資料*停止保護*狀態張貼成功完成**停止備份**作業：

1. 瀏覽 toohello**受保護項目**頁面，然後選取**Azure 虛擬機器**為*類型*按一下 hello**選取** 按鈕。

    ![VM 類型](./media/backup-azure-manage-vms/vm-type.png)
2. 選取 hello 虛擬機器。 hello 虛擬機器會處於**停止保護**狀態。

    ![已停止保護](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. 按一下 hello**刪除**在 hello hello 頁面底部的按鈕。

    ![刪除備份](./media/backup-azure-manage-vms/delete-backup.png)
4. 在 [hello**刪除備份資料**精靈] 中，選取刪除 （強烈建議） 備份資料的原因，然後按一下**送出**。

    ![刪除備份資料](./media/backup-azure-manage-vms/delete-backup-data.png)
5. 這會建立選取的虛擬機器作業 toodelete 備份資料。 按一下**檢視工作**toosee 作業 頁面中相對應的工作。

    ![成功刪除資料](./media/backup-azure-manage-vms/delete-data-success.png)

    Hello 作業完成後，hello 對應 toohello 虛擬機器會移除的項目**受保護項目**頁面。

## <a name="dashboard"></a>儀表板
在 hello**儀表板**頁面上，您可以檢閱 Azure 虛擬機器、 儲存和與其相關聯 hello 在過去 24 小時內的工作的相關資訊。 您可以檢視備份狀態和任何相關聯的備份錯誤。

![儀表板](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Hello 儀表板中的值，就會重新整理一次每隔 24 小時。
>
>

## <a name="auditing-operations"></a>稽核作業
Azure 備份提供 hello"作業記錄 」 備份作業的 hello 客戶，讓您輕鬆 toosee hello 備份保存庫執行完全管理作業所觸發的檢閱。 作業記錄檔啟用絕佳的檢討，和稽核 hello 備份作業的支援。

下列作業的 hello 會記錄在作業記錄：

* 註冊
* Unregister 
* 設定保護
* 備份 (同時透過 BackupNow 進行排程以及隨選備份)
* 還原
* 停止保護
* 刪除備份資料
* Add policy
* 刪除原則
* 更新原則
* 取消工作

tooview 作業記錄檔對應 tooa 備份保存庫：

1. 瀏覽過**管理服務**在 Azure 入口網站，然後按一下hello**作業記錄** 索引標籤。

    ![作業記錄](./media/backup-azure-manage-vms/ops-logs.png)
2. 在 hello 篩選條件中，選取**備份**為*類型*hello 備份保存庫中指定名稱和*服務名稱*，然後按一下 **送出**。

    ![作業記錄檔篩選器](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Hello 作業記錄檔、 選取任何作業，然後按一下**詳細資料**toosee 詳細說明對應 tooan 作業。

    ![作業記錄檔擷取詳細資料](./media/backup-azure-manage-vms/ops-logs-details.png)

    hello**明細 精靈中**包含 hello 作業觸發，作業識別碼，資源的這項作業會觸發並 hello 作業的開始時間的相關資訊。

    ![Operation Details](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>警示通知
您可以在入口網站取得 hello 工作的自訂警示通知。 這是藉由在作業記錄檔事件中定義以 PowerShell 為基礎的警示規則來達成。 我們建議使用「PowerShell 1.3.0 版或更新版本」 。

toodefine 備份失敗的自訂通知 tooalert，範例命令看起來像：

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**：您可從以上章節所述的 [作業記錄檔] 快顯視窗中取得。 作業的詳細資料快顯視窗中的 ResourceUri 是 hello ResourceId toobe 提供給這個指令程式。

**OperationName**： 這會是 hello 格式的"Microsoft.Backup/backupvault/<EventName>"其中 EventName 是其中一個暫存器、 取消註冊、 ConfigureProtection、 備份、 還原、 StopProtection、 DeleteBackupData，CreateProtectionPolicy，DeleteProtectionPolicy，UpdateProtectionPolicy

**狀態**：支援的值為 - 已開始、成功和失敗。

**ResourceGroup**: hello 資源在其觸發作業的資源群組。 您可以從 ResourceId 值加以取得。 值，欄位之間*/resourceGroups/*和*/providers/* ResourceId 中值為 hello ResourceGroup 值。

**名稱**: hello 警示規則的名稱。

**CustomEmail**： 指定您想要 toosend 警示通知的 hello 自訂電子郵件地址 toowhich

**SendToServiceOwners**： 這個選項會傳送警示通知 tooall 系統管理員和共同管理員的 hello 訂用帳戶。 它可以用於 **New-AzureRmAlertRuleEmail** Cmdlet 中

### <a name="limitations-on-alerts"></a>警示的限制
以事件為基礎的警示會受到 toohello 下列限制：

1. Hello 備份保存庫中的所有虛擬機器上便會觸發警示。 您無法自訂 tooget 組特定的備份保存庫中的虛擬機器的警示。
2. 這項功能處於預覽狀態。 [深入了解](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. 您將會收到來自 "alerts-noreply@mail.windowsazure.com" 的警示。 目前您無法修改 hello 電子郵件寄件者。

## <a name="next-steps"></a>後續步驟
* [還原 Azure VM](backup-azure-restore-vms.md)
