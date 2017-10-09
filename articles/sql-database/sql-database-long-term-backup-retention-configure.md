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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="a98ac-103">設定 Azure SQL Database 長期備份保留並從中還原</span><span class="sxs-lookup"><span data-stu-id="a98ac-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="a98ac-104">您可以設定 hello Azure 復原服務保存庫 toostore Azure SQL 資料庫備份，然後使用備份的資料庫保留在 hello 保存庫使用的復原 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a98ac-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="a98ac-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a98ac-105">Azure portal</span></span>

<span data-ttu-id="a98ac-106">下列各節顯示如何 toouse hello Azure 入口網站 tooconfigure hello Azure 復原服務保存庫，您在 hello 保存庫中，檢視備份和還原 hello 保存庫中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a98ac-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="a98ac-107">設定 hello 保存庫，註冊 hello 伺服器，然後選取資料庫</span><span class="sxs-lookup"><span data-stu-id="a98ac-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="a98ac-108">您[設定 Azure 復原服務保存庫 tooretain 自動化備份](sql-database-long-term-retention.md)hello 服務層的保留期限超過一段時間。</span><span class="sxs-lookup"><span data-stu-id="a98ac-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="a98ac-109">開啟 hello **SQL Server**頁面為您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a98ac-109">Open hello **SQL Server** page for your server.</span></span>

   ![SQL Server 頁面](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="a98ac-111">按一下 [長期備份保留]。</span><span class="sxs-lookup"><span data-stu-id="a98ac-111">Click **Long-term backup retention**.</span></span>

   ![長期備份保留連結](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="a98ac-113">在 hello**長期備份的保留**伺服器頁面上，檢閱並接受 hello 預覽條款 （除非您已完成，-，或這項功能不會再為預覽狀態）。</span><span class="sxs-lookup"><span data-stu-id="a98ac-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![接受 hello 預覽條款](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="a98ac-115">長期備份保留 tooconfigure，hello 方格中選取該資料庫，然後按一下**設定**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="a98ac-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![選取長期備份保留的資料庫](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="a98ac-117">在 hello**設定**頁面上，按一下**設定必要設定**下**復原服務保存庫**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![設定保存庫連結](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="a98ac-119">在 hello**復原服務保存庫**頁面上，選取現有的保存庫，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="a98ac-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="a98ac-120">否則，如果找到訂用帳戶沒有復原服務保存庫，按一下 tooexit hello 流程，並建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![建立保存庫連結](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="a98ac-122">在 hello**復原服務保存庫**頁面上，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![新增保存庫連結](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="a98ac-124">在 hello**復原服務保存庫**頁面上，提供有效的名稱，如 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![新增保存庫名稱](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="a98ac-126">選取您的訂用帳戶和資源群組，然後選取 hello hello 保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="a98ac-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="a98ac-127">完成時，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a98ac-127">When done, click **Create**.</span></span>

   ![建立保存庫](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="a98ac-129">hello 保存庫必須位在 hello 與 hello SQL Azure 邏輯伺服器相同的區域，並使用必須 hello 相同 hello 邏輯伺服器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a98ac-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="a98ac-130">建立 hello 新保存庫之後，執行 hello 必要步驟 tooreturn toohello**復原服務保存庫**頁面。</span><span class="sxs-lookup"><span data-stu-id="a98ac-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="a98ac-131">在 hello**復原服務保存庫**頁面上，按一下 hello 保存庫，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![選取現有的保存庫](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="a98ac-133">在 hello**設定**頁面上，提供有效的名稱 hello 新保留原則、 修改為適當且 hello 預設保留原則，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="a98ac-135">Hello 上**長期備份的保留**為您的資料庫頁面上，按一下**儲存**，然後按一下**確定**tooapply hello 長期備份保留原則 tooall 選取資料庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="a98ac-137">按一下**儲存**tooenable 長期的備份保留使用這個新原則 toohello Azure 復原服務保存庫設定。</span><span class="sxs-lookup"><span data-stu-id="a98ac-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="a98ac-139">一旦設定之後，備份會顯示在 hello 保存庫內接下來七天。</span><span class="sxs-lookup"><span data-stu-id="a98ac-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="a98ac-140">等到備份顯示在 hello 保存庫，再繼續本教學課程。</span><span class="sxs-lookup"><span data-stu-id="a98ac-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="a98ac-141">使用 Azure 入口網站在長期保留期限中檢視備份</span><span class="sxs-lookup"><span data-stu-id="a98ac-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="a98ac-142">檢視[長期備份保留](sql-database-long-term-retention.md)中資料庫備份的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a98ac-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="a98ac-143">在 hello Azure 入口網站中開啟您的 Azure 復原服務保存庫，針對資料庫備份 (跳過**所有資源**和選取從您的訂用帳戶資源 hello 清單) 您的資料庫所使用的儲存體 tooview hello 數量hello 保存庫中的備份。</span><span class="sxs-lookup"><span data-stu-id="a98ac-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![使用備份檢視復原服務保存庫](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="a98ac-145">開啟 hello **SQL database**資料庫的頁面。</span><span class="sxs-lookup"><span data-stu-id="a98ac-145">Open hello **SQL database** page for your database.</span></span>

   ![新範例 DB 頁面](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="a98ac-147">在 [hello] 工具列上按一下**還原**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-147">On hello toolbar, click **Restore**.</span></span>

   ![還原工具列](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="a98ac-149">在 hello 還原 頁面上，按一下 **長期**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="a98ac-150">按一下 Azure 保存庫備份**選取的備份**tooview hello 可用的資料庫備份，在長期備份的保留。</span><span class="sxs-lookup"><span data-stu-id="a98ac-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![保存庫中的備份](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="a98ac-152">長期備份的保留使用 hello Azure 入口網站中從備份還原資料庫</span><span class="sxs-lookup"><span data-stu-id="a98ac-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="a98ac-153">您從 hello Azure 復原服務保存庫中的備份還原 hello tooa 新資料庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="a98ac-154">在 hello **Azure 保存庫備份**頁面上，按一下 hello 備份 toorestore，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="a98ac-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![選取保存庫中的備份](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="a98ac-156">在 hello**資料庫名稱**文字方塊中，提供 hello hello 還原資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="a98ac-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![新的資料庫名稱](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="a98ac-158">按一下**確定**toorestore 從 hello 保存庫 toohello 新資料庫中的 hello 備份資料庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="a98ac-159">Hello 工具列上，按一下 hello 通知圖示 tooview hello hello 還原工作狀態。</span><span class="sxs-lookup"><span data-stu-id="a98ac-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![從保存庫還原作業進度](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="a98ac-161">Hello 還原作業完成後，開啟 hello **SQL 資料庫**頁面 tooview hello 最近還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![從保存庫還原的資料庫](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="a98ac-163">您可以從這裡連接 toohello 還原資料庫使用 SQL Server Management Studio tooperform 所需的工作，例如太[hello 還原資料庫 toocopy 的位元的資料擷取到 hello 現有的資料庫或現有的 toodelete hello資料庫和重新命名 hello 還原資料庫 toohello 現有的資料庫名稱](sql-database-recovery-using-backups.md#point-in-time-restore)。</span><span class="sxs-lookup"><span data-stu-id="a98ac-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="a98ac-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a98ac-164">PowerShell</span></span>

<span data-ttu-id="a98ac-165">hello 下列各節會顯示 toouse PowerShell tooconfigure hello Azure 復原服務保存庫，在 hello 保存庫中，檢視備份與還原 hello 保存庫中的方式。</span><span class="sxs-lookup"><span data-stu-id="a98ac-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a98ac-166">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="a98ac-166">Create a recovery services vault</span></span>

<span data-ttu-id="a98ac-167">使用 hello[新增 AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a98ac-168">hello 保存庫必須位在 hello 與 hello SQL Azure 邏輯伺服器相同的區域，並使用必須 hello 相同 hello 邏輯伺服器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a98ac-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="a98ac-169">為其長期保留的備份設定您伺服器 toouse hello 復原保存庫</span><span class="sxs-lookup"><span data-stu-id="a98ac-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="a98ac-170">使用 hello[組 AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault)先前建立的 cmdlet tooassociate 復原服務保存庫與特定的 Azure SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a98ac-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="a98ac-171">建立保留原則</span><span class="sxs-lookup"><span data-stu-id="a98ac-171">Create a retention policy</span></span>

<span data-ttu-id="a98ac-172">保留原則就是您設定多久 tookeep 資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="a98ac-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="a98ac-173">使用 hello [Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello 預設保留原則 toouse 當做 hello 範本建立原則。</span><span class="sxs-lookup"><span data-stu-id="a98ac-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="a98ac-174">此範本中 hello 保留期限設定為 2 年。</span><span class="sxs-lookup"><span data-stu-id="a98ac-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="a98ac-175">接下來，執行 hello[新增 AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally 建立 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="a98ac-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="a98ac-176">部分指令程式需要您設定 hello 保存庫內容，再執行 ([組 AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) 讓您查看幾個相關的程式碼片段中的這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="a98ac-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="a98ac-177">因為 hello 原則是 hello 保存庫的一部分，您可以設定 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="a98ac-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="a98ac-178">您可以建立多個保留原則，針對每個保存庫，然後再套用所需的 hello 原則 toospecific 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="a98ac-179">設定資料庫 toouse hello 預先定義保留原則</span><span class="sxs-lookup"><span data-stu-id="a98ac-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="a98ac-180">使用 hello[組 AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello 新原則 tooa 特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="a98ac-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="a98ac-181">檢視備份資訊和長期保留中的備份</span><span class="sxs-lookup"><span data-stu-id="a98ac-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="a98ac-182">檢視[長期備份保留](sql-database-long-term-retention.md)中資料庫備份的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a98ac-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="a98ac-183">使用下列 cmdlet tooview 備份資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="a98ac-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="a98ac-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="a98ac-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="a98ac-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="a98ac-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="a98ac-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="a98ac-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="a98ac-187">從長期備份保留備份中還原資料庫</span><span class="sxs-lookup"><span data-stu-id="a98ac-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="a98ac-188">還原從長期備份的保留使用 hello[還原 AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a98ac-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="a98ac-189">從這裡，您可以連接 toohello 還原資料庫使用 SQL Server Management Studio tooperform 所需的工作，例如 tooextract 的 hello 資料位元，請還原到 hello 現有的資料庫或 toodelete hello 現有的資料庫和重新命名的資料庫 toocopyhello 還原的資料庫 toohello 現有的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a98ac-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="a98ac-190">請參閱[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)。</span><span class="sxs-lookup"><span data-stu-id="a98ac-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a98ac-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a98ac-191">Next steps</span></span>

- <span data-ttu-id="a98ac-192">toolearn 有關服務產生的自動備份，請參閱[自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="a98ac-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="a98ac-193">toolearn 有關長期備份的保留，請參閱[長期備份的保留](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="a98ac-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="a98ac-194">請參閱有關從備份還原 toolearn[從備份還原](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="a98ac-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
