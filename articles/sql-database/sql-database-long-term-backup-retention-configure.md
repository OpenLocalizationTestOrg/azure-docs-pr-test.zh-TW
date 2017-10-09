---
title: "設定長期備份保留 - Azure SQL Database | Microsoft Docs"
description: "了解 toostore 自動化的 hello Azure 復原服務保存庫中的備份的方式，並從 hello toorestore Azure 復原服務保存庫"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>設定 Azure SQL Database 長期備份保留並從中還原

您可以設定 hello Azure 復原服務保存庫 toostore Azure SQL 資料庫備份，然後使用備份的資料庫保留在 hello 保存庫使用的復原 hello Azure 入口網站或 PowerShell。

## <a name="azure-portal"></a>Azure 入口網站

下列各節顯示如何 toouse hello Azure 入口網站 tooconfigure hello Azure 復原服務保存庫，您在 hello 保存庫中，檢視備份和還原 hello 保存庫中的 hello。

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>設定 hello 保存庫，註冊 hello 伺服器，然後選取資料庫

您[設定 Azure 復原服務保存庫 tooretain 自動化備份](sql-database-long-term-retention.md)hello 服務層的保留期限超過一段時間。 

1. 開啟 hello **SQL Server**頁面為您的伺服器。

   ![SQL Server 頁面](./media/sql-database-get-started-portal/sql-server-blade.png)

2. 按一下 [長期備份保留]。

   ![長期備份保留連結](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. 在 hello**長期備份的保留**伺服器頁面上，檢閱並接受 hello 預覽條款 （除非您已完成，-，或這項功能不會再為預覽狀態）。

   ![接受 hello 預覽條款](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. 長期備份保留 tooconfigure，hello 方格中選取該資料庫，然後按一下**設定**hello 工具列上。

   ![選取長期備份保留的資料庫](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. 在 hello**設定**頁面上，按一下**設定必要設定**下**復原服務保存庫**。

   ![設定保存庫連結](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. 在 hello**復原服務保存庫**頁面上，選取現有的保存庫，如果有的話。 否則，如果找到訂用帳戶沒有復原服務保存庫，按一下 tooexit hello 流程，並建立復原服務保存庫。

   ![建立保存庫連結](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. 在 hello**復原服務保存庫**頁面上，按一下**新增**。

   ![新增保存庫連結](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. 在 hello**復原服務保存庫**頁面上，提供有效的名稱，如 hello 復原服務保存庫。

   ![新增保存庫名稱](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. 選取您的訂用帳戶和資源群組，然後選取 hello hello 保存庫的位置。 完成時，按一下 [建立]。

   ![建立保存庫](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > hello 保存庫必須位在 hello 與 hello SQL Azure 邏輯伺服器相同的區域，並使用必須 hello 相同 hello 邏輯伺服器的資源群組。
   >

10. 建立 hello 新保存庫之後，執行 hello 必要步驟 tooreturn toohello**復原服務保存庫**頁面。

11. 在 hello**復原服務保存庫**頁面上，按一下 hello 保存庫，然後按一下**選取**。

   ![選取現有的保存庫](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. 在 hello**設定**頁面上，提供有效的名稱 hello 新保留原則、 修改為適當且 hello 預設保留原則，然後按一下**確定**。

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. Hello 上**長期備份的保留**為您的資料庫頁面上，按一下**儲存**，然後按一下**確定**tooapply hello 長期備份保留原則 tooall 選取資料庫。

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. 按一下**儲存**tooenable 長期的備份保留使用這個新原則 toohello Azure 復原服務保存庫設定。

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> 一旦設定之後，備份會顯示在 hello 保存庫內接下來七天。 等到備份顯示在 hello 保存庫，再繼續本教學課程。
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>使用 Azure 入口網站在長期保留期限中檢視備份

檢視[長期備份保留](sql-database-long-term-retention.md)中資料庫備份的相關資訊。 

1. 在 hello Azure 入口網站中開啟您的 Azure 復原服務保存庫，針對資料庫備份 (跳過**所有資源**和選取從您的訂用帳戶資源 hello 清單) 您的資料庫所使用的儲存體 tooview hello 數量hello 保存庫中的備份。

   ![使用備份檢視復原服務保存庫](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. 開啟 hello **SQL database**資料庫的頁面。

   ![新範例 DB 頁面](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. 在 [hello] 工具列上按一下**還原**。

   ![還原工具列](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. 在 hello 還原 頁面上，按一下 **長期**。

5. 按一下 Azure 保存庫備份**選取的備份**tooview hello 可用的資料庫備份，在長期備份的保留。

   ![保存庫中的備份](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>長期備份的保留使用 hello Azure 入口網站中從備份還原資料庫

您從 hello Azure 復原服務保存庫中的備份還原 hello tooa 新資料庫。

1. 在 hello **Azure 保存庫備份**頁面上，按一下 hello 備份 toorestore，然後按一下**選取**。

   ![選取保存庫中的備份](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. 在 hello**資料庫名稱**文字方塊中，提供 hello hello 還原資料庫的名稱。

   ![新的資料庫名稱](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. 按一下**確定**toorestore 從 hello 保存庫 toohello 新資料庫中的 hello 備份資料庫。

4. Hello 工具列上，按一下 hello 通知圖示 tooview hello hello 還原工作狀態。

   ![從保存庫還原作業進度](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Hello 還原作業完成後，開啟 hello **SQL 資料庫**頁面 tooview hello 最近還原的資料庫。

   ![從保存庫還原的資料庫](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> 您可以從這裡連接 toohello 還原資料庫使用 SQL Server Management Studio tooperform 所需的工作，例如太[hello 還原資料庫 toocopy 的位元的資料擷取到 hello 現有的資料庫或現有的 toodelete hello資料庫和重新命名 hello 還原資料庫 toohello 現有的資料庫名稱](sql-database-recovery-using-backups.md#point-in-time-restore)。
>

## <a name="powershell"></a>PowerShell

hello 下列各節會顯示 toouse PowerShell tooconfigure hello Azure 復原服務保存庫，在 hello 保存庫中，檢視備份與還原 hello 保存庫中的方式。

### <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

使用 hello[新增 AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate 復原服務保存庫。

> [!IMPORTANT]
> hello 保存庫必須位在 hello 與 hello SQL Azure 邏輯伺服器相同的區域，並使用必須 hello 相同 hello 邏輯伺服器的資源群組。

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>為其長期保留的備份設定您伺服器 toouse hello 復原保存庫

使用 hello[組 AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault)先前建立的 cmdlet tooassociate 復原服務保存庫與特定的 Azure SQL 伺服器。

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>建立保留原則

保留原則就是您設定多久 tookeep 資料庫備份。 使用 hello [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello 預設保留原則 toouse 當做 hello 範本建立原則。 此範本中 hello 保留期限設定為 2 年。 接下來，執行 hello[新增 AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally 建立 hello 原則。 

> [!NOTE]
> 部分指令程式需要您設定 hello 保存庫內容，再執行 ([組 AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) 讓您查看幾個相關的程式碼片段中的這個指令程式。 因為 hello 原則是 hello 保存庫的一部分，您可以設定 hello 內容。 您可以建立多個保留原則，針對每個保存庫，然後再套用所需的 hello 原則 toospecific 資料庫。 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>設定資料庫 toouse hello 預先定義保留原則

使用 hello[組 AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello 新原則 tooa 特定資料庫。

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>檢視備份資訊和長期保留中的備份

檢視[長期備份保留](sql-database-long-term-retention.md)中資料庫備份的相關資訊。 

使用下列 cmdlet tooview 備份資訊的 hello:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>從長期備份保留備份中還原資料庫

還原從長期備份的保留使用 hello[還原 AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet。

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> 從這裡，您可以連接 toohello 還原資料庫使用 SQL Server Management Studio tooperform 所需的工作，例如 tooextract 的 hello 資料位元，請還原到 hello 現有的資料庫或 toodelete hello 現有的資料庫和重新命名的資料庫 toocopyhello 還原的資料庫 toohello 現有的資料庫名稱。 請參閱[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)。

## <a name="next-steps"></a>後續步驟

- toolearn 有關服務產生的自動備份，請參閱[自動備份](sql-database-automated-backups.md)
- toolearn 有關長期備份的保留，請參閱[長期備份的保留](sql-database-long-term-retention.md)
- 請參閱有關從備份還原 toolearn[從備份還原](sql-database-recovery-using-backups.md)
