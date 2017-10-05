---
title: "設定長期備份保留 - Azure SQL Database | Microsoft Docs"
description: "了解如何從在 Azure 復原服務保存庫中儲存自動備份，以及從 Azure 復原服務保存庫還原"
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
ms.openlocfilehash: ed9f74a59f0ca512e2758c6db4c5c9075030f859
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="6b596-103">設定 Azure SQL Database 長期備份保留並從中還原</span><span class="sxs-lookup"><span data-stu-id="6b596-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="6b596-104">您可以設定 Azure 復原服務保存庫以存放 Azure SQL 資料庫備份，然後使用透過 Azure 入口網站或 PowerShell 保留在保存庫中的備份，來復原資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="6b596-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6b596-105">Azure portal</span></span>

<span data-ttu-id="6b596-106">下列幾節中會示範如何使用 Azure 入口網站來設定 Azure 復原服務保存庫、檢視保存庫中的備份，以及從保存庫中還原。</span><span class="sxs-lookup"><span data-stu-id="6b596-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="6b596-107">設定保存庫、註冊伺服器及選取資料庫</span><span class="sxs-lookup"><span data-stu-id="6b596-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="6b596-108">您會[設定 Azure 復原服務保存庫以保留自動備份](sql-database-long-term-retention.md)，時間較您服務層的保留期限長。</span><span class="sxs-lookup"><span data-stu-id="6b596-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

1. <span data-ttu-id="6b596-109">開啟您伺服器的 **SQL Server** 頁面。</span><span class="sxs-lookup"><span data-stu-id="6b596-109">Open the **SQL Server** page for your server.</span></span>

   ![SQL Server 頁面](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="6b596-111">按一下 [長期備份保留]。</span><span class="sxs-lookup"><span data-stu-id="6b596-111">Click **Long-term backup retention**.</span></span>

   ![長期備份保留連結](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="6b596-113">在伺服器的 [長期備份保留] 頁面中，檢閱並接受預覽條款 (除非您已完成，或預覽中沒有這項功能)。</span><span class="sxs-lookup"><span data-stu-id="6b596-113">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![接受預覽條款](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="6b596-115">若要設定長期備份保留時間，在方格中選取該資料庫，然後按一下工具列上的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="6b596-115">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![選取長期備份保留的資料庫](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="6b596-117">在 [設定] 頁面上，按一下 [復原服務保存庫] 下的 [設定所需設定]。</span><span class="sxs-lookup"><span data-stu-id="6b596-117">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![設定保存庫連結](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="6b596-119">在 [復原服務保存庫] 頁面中，選取現有的保存庫 (若有)。</span><span class="sxs-lookup"><span data-stu-id="6b596-119">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="6b596-120">否則，如果找不到您訂用帳戶的復原服務保存庫，按一下以結束流程，並建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-120">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![建立保存庫連結](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="6b596-122">在 [復原服務保存庫] 頁面上，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6b596-122">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![新增保存庫連結](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="6b596-124">在 [復原服務保存庫] 頁面上，提供復原服務保存庫的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="6b596-124">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![新增保存庫名稱](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="6b596-126">選取您的訂用帳戶和資源群組，然後選取保存庫的位置。</span><span class="sxs-lookup"><span data-stu-id="6b596-126">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="6b596-127">完成時，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6b596-127">When done, click **Create**.</span></span>

   ![建立保存庫](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="6b596-129">保存庫必須位於與 Azure SQL 邏輯伺服器相同的區域，而且必須使用相同的資源群組做為邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="6b596-129">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="6b596-130">建立新的保存庫之後，執行必要的步驟以返回 [復原服務保存庫] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6b596-130">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="6b596-131">在 [復原服務保存庫] 頁面上，按一下保存庫，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="6b596-131">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![選取現有的保存庫](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="6b596-133">在 [設定] 頁面上，提供新保留原則的有效名稱、適當修改預設保留原則，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6b596-133">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="6b596-135">在伺服器的 [長期備份保留] 頁面上，按一下 [儲存]，然後按一下 [確定]，將長期備份保留原則套用到所有選取的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-135">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="6b596-137">按一下 [儲存] 以使用這個新的原則對您所設定的 Azure 復原服務保存庫啟用長期備份保留。</span><span class="sxs-lookup"><span data-stu-id="6b596-137">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![定義保留原則](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="6b596-139">設定之後，備份會在接下來七天內顯示於保存庫中。</span><span class="sxs-lookup"><span data-stu-id="6b596-139">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="6b596-140">備份出現在保存庫之前，請勿繼續本教學課程。</span><span class="sxs-lookup"><span data-stu-id="6b596-140">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="6b596-141">使用 Azure 入口網站在長期保留期限中檢視備份</span><span class="sxs-lookup"><span data-stu-id="6b596-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="6b596-142">檢視[長期備份保留](sql-database-long-term-retention.md)中資料庫備份的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6b596-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="6b596-143">在 Azure 入口網站中，開啟資料庫備份的 Azure 復原服務保存庫 (移至 [所有資源]，並從您訂用帳戶的資源清單中選取)，以在保存庫中檢視資料庫備份所使用的儲存體數量。</span><span class="sxs-lookup"><span data-stu-id="6b596-143">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![使用備份檢視復原服務保存庫](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="6b596-145">開啟您資料庫的 [SQL Database] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6b596-145">Open the **SQL database** page for your database.</span></span>

   ![新範例 DB 頁面](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="6b596-147">在工具列上，按一下 [還原]。</span><span class="sxs-lookup"><span data-stu-id="6b596-147">On the toolbar, click **Restore**.</span></span>

   ![還原工具列](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="6b596-149">在 [還原] 頁面上，按一下 [長期]。</span><span class="sxs-lookup"><span data-stu-id="6b596-149">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="6b596-150">在 Azure 保存庫備份下，按一下 [選取備份]，在長期備份保留中檢視可用的資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="6b596-150">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![保存庫中的備份](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="6b596-152">使用 Azure 入口網站從長期備份保留的備份中還原資料庫</span><span class="sxs-lookup"><span data-stu-id="6b596-152">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="6b596-153">從 Azure 復原服務保存庫中的備份將資料庫還原到新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-153">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="6b596-154">在 [Azure 保存庫備份] 頁面上，按一下要還原的備份，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="6b596-154">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![選取保存庫中的備份](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="6b596-156">在 [資料庫名稱] 文字方塊中，提供還原的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="6b596-156">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![新的資料庫名稱](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="6b596-158">按一下 [確定]，從保存庫中的備份將資料庫還原到新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-158">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="6b596-159">在工具列上，按一下 [通知] 圖示以檢視還原作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="6b596-159">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![從保存庫還原作業進度](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="6b596-161">完成還原作業之後，開啟 [SQL Database] 頁面，以檢視剛還原的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-161">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![從保存庫還原的資料庫](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="6b596-163">從這裡開始，您可以使用 SQL Server Management Studio 連接到已還原的資料庫來執行所需的工作，例如[從還原的資料庫擷取一堆資料來複製到現有的資料庫，或刪除現有的資料庫，並將還原的資料庫重新命名為現有的資料庫名稱](sql-database-recovery-using-backups.md#point-in-time-restore)。</span><span class="sxs-lookup"><span data-stu-id="6b596-163">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="6b596-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b596-164">PowerShell</span></span>

<span data-ttu-id="6b596-165">下列幾節中會示範如何使用 PowerShell 來設定 Azure 復原服務保存庫、檢視保存庫中的備份，以及從保存庫中還原。</span><span class="sxs-lookup"><span data-stu-id="6b596-165">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6b596-166">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="6b596-166">Create a recovery services vault</span></span>

<span data-ttu-id="6b596-167">使用 [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) 來建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-167">Use the [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b596-168">保存庫必須位於與 Azure SQL 邏輯伺服器相同的區域，而且必須使用相同的資源群組做為邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="6b596-168">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="6b596-169">設定您的伺服器設以將復原保存庫用於其長期保留備份</span><span class="sxs-lookup"><span data-stu-id="6b596-169">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="6b596-170">使用 [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) Cmdlet，讓先前建立的復原服務保存庫與特定 Azure SQL Server 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6b596-170">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="6b596-171">建立保留原則</span><span class="sxs-lookup"><span data-stu-id="6b596-171">Create a retention policy</span></span>

<span data-ttu-id="6b596-172">保留原則就是您設定資料庫備份保留時間長度的位置。</span><span class="sxs-lookup"><span data-stu-id="6b596-172">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="6b596-173">使用 [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) Cmdlet 來取得預設保留原則，以便作為建立原則的範本。</span><span class="sxs-lookup"><span data-stu-id="6b596-173">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="6b596-174">在此範本中，保留期限設定為 2 年。</span><span class="sxs-lookup"><span data-stu-id="6b596-174">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="6b596-175">接下來，執行 [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) 完成原則建立。</span><span class="sxs-lookup"><span data-stu-id="6b596-175">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="6b596-176">有些 Cmdlet 會要求您先設定保存庫內容，然後才執行 ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext))，所以您會在幾個相關的程式碼片段中看見此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6b596-176">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="6b596-177">因為原則是保存庫的一部分，所以我們會設定內容。</span><span class="sxs-lookup"><span data-stu-id="6b596-177">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="6b596-178">您可以為每個保存庫建立多個保留原則，然後將所需的原則套用到特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-178">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="6b596-179">設定資料庫以使用先前定義的保留原則</span><span class="sxs-lookup"><span data-stu-id="6b596-179">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="6b596-180">使用 [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) Cmdlet，將新原則套用到特定資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b596-180">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="6b596-181">檢視備份資訊和長期保留中的備份</span><span class="sxs-lookup"><span data-stu-id="6b596-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="6b596-182">檢視[長期備份保留](sql-database-long-term-retention.md)中資料庫備份的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6b596-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="6b596-183">請使用下列 Cmdlet 來檢視備份資訊︰</span><span class="sxs-lookup"><span data-stu-id="6b596-183">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="6b596-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="6b596-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="6b596-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="6b596-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="6b596-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="6b596-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="6b596-187">從長期備份保留備份中還原資料庫</span><span class="sxs-lookup"><span data-stu-id="6b596-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="6b596-188">使用 [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) Cmdlet 從長期備份保留中還原。</span><span class="sxs-lookup"><span data-stu-id="6b596-188">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
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
> <span data-ttu-id="6b596-189">從這裡開始，您可以使用 SQL Server Management Studio 連線到已還原的資料庫來執行所需的工作，例如從還原的資料庫擷取一堆資料來複製到現有的資料庫，或刪除現有的資料庫，並將還原的資料庫重新命名為現有的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="6b596-189">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name.</span></span> <span data-ttu-id="6b596-190">請參閱[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)。</span><span class="sxs-lookup"><span data-stu-id="6b596-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b596-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b596-191">Next steps</span></span>

- <span data-ttu-id="6b596-192">若要深入了解服務產生的自動備份，請參閱[自動備份](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="6b596-192">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="6b596-193">若要深入了解長期備份保留，請參閱[長期備份保留](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="6b596-193">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="6b596-194">若要深入了解從備份還原，請參閱[從備份還原](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="6b596-194">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
