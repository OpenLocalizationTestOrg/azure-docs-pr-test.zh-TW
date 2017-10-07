---
title: "Azure SQL database tooa BACPAC 檔案 aaaExport |Microsoft 文件"
description: "使用 Azure 入口網站 hello Azure SQL database tooa BACPAC 檔案匯出"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a><span data-ttu-id="91555-103">Azure SQL database tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="91555-103">Export an Azure SQL database tooa BACPAC file</span></span>

<span data-ttu-id="91555-104">當您需要 tooexport 資料庫，為了封存或移動 tooanother 平台時，您可以匯出 hello 資料庫結構描述和資料 tooa [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)檔案。</span><span class="sxs-lookup"><span data-stu-id="91555-104">When you need tooexport a database for archiving or for moving tooanother platform, you can export hello database schema and data tooa [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="91555-105">BACPAC 檔案是包含 hello 中繼資料和資料從 SQL Server 資料庫的 BACPAC 的延伸模組 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="91555-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="91555-106">BACPAC 檔案可以儲存在 Azure Blob 儲存體，或在內部部署位置的本機儲存體中，之後再匯入至 Azure SQL Database 或 SQL Server 內部部署安裝。</span><span class="sxs-lookup"><span data-stu-id="91555-106">A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="91555-107">Azure SQL Database 自動匯出已在 2017 年 3 月 1 日淘汰。</span><span class="sxs-lookup"><span data-stu-id="91555-107">Azure SQL Database Automated Export was retired on March 1, 2017.</span></span> <span data-ttu-id="91555-108">您可以使用[長期備份的保留](sql-database-long-term-retention.md
)或[Azure 自動化](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md)tooperiodically 封存的 SQL 資料庫使用 PowerShell，根據您選擇的 tooa 排程。</span><span class="sxs-lookup"><span data-stu-id="91555-108">You can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) tooperiodically archive SQL databases using PowerShell according tooa schedule of your choice.</span></span> <span data-ttu-id="91555-109">如需範例，請下載 hello[範例 PowerShell 指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)從 Github。</span><span class="sxs-lookup"><span data-stu-id="91555-109">For a sample, download hello [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span></span>
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a><span data-ttu-id="91555-110">匯出 Azure SQL Database 時的考量</span><span class="sxs-lookup"><span data-stu-id="91555-110">Considerations when exporting an Azure SQL database</span></span>

* <span data-ttu-id="91555-111">匯出 toobe 具有交易一致性，您必須確定任一 hello 在匯出期間，正在發生之任何寫入活動，或者您要匯出從[交易一致性複本](sql-database-copy.md)您的 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="91555-111">For an export toobe transactionally consistent, you must ensure either that no write activity is occurring during hello export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.</span></span>
* <span data-ttu-id="91555-112">如果您正在匯出 tooblob 儲存體，hello BACPAC 檔案的大小上限為 200 GB。</span><span class="sxs-lookup"><span data-stu-id="91555-112">If you are exporting tooblob storage, hello maximum size of a BACPAC file is 200 GB.</span></span> <span data-ttu-id="91555-113">tooarchive 較大的 BACPAC 檔案匯出 toolocal 儲存體。</span><span class="sxs-lookup"><span data-stu-id="91555-113">tooarchive a larger BACPAC file, export toolocal storage.</span></span>
* <span data-ttu-id="91555-114">不支援匯出 BACPAC 檔案 tooAzure 高階儲存體使用本文所討論的 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="91555-114">Exporting a BACPAC file tooAzure premium storage using hello methods discussed in this article is not supported.</span></span>
* <span data-ttu-id="91555-115">如果從 Azure SQL Database 的 hello 匯出作業超過 20 小時，它可能會取消。</span><span class="sxs-lookup"><span data-stu-id="91555-115">If hello export operation from Azure SQL Database exceeds 20 hours, it may be canceled.</span></span> <span data-ttu-id="91555-116">在匯出期間 tooincrease 效能，您可以：</span><span class="sxs-lookup"><span data-stu-id="91555-116">tooincrease performance during export, you can:</span></span>
  * <span data-ttu-id="91555-117">暫時提高您的服務等級。</span><span class="sxs-lookup"><span data-stu-id="91555-117">Temporarily increase your service level.</span></span>
  * <span data-ttu-id="91555-118">停止所有讀取及寫入 hello 匯出期間的活動。</span><span class="sxs-lookup"><span data-stu-id="91555-118">Cease all read and write activity during hello export.</span></span>
  * <span data-ttu-id="91555-119">在所有大型資料表上搭配使用 [叢集索引](https://msdn.microsoft.com/library/ms190457.aspx) 和非 null 值。</span><span class="sxs-lookup"><span data-stu-id="91555-119">Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables.</span></span> <span data-ttu-id="91555-120">若沒有叢集索引，如果要花超過 6-12 小時，匯出可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="91555-120">Without clustered indexes, an export may fail if it takes longer than 6-12 hours.</span></span> <span data-ttu-id="91555-121">這是因為 hello 匯出服務需要 toocomplete 資料表掃描 tootry tooexport 整個資料表。</span><span class="sxs-lookup"><span data-stu-id="91555-121">This is because hello export service needs toocomplete a table scan tootry tooexport entire table.</span></span> <span data-ttu-id="91555-122">如果匯出為 toorun 最佳化資料表的好方法 toodetermine **DBCC SHOW_STATISTICS** ，並確定該 hello *RANGE_HI_KEY*不是 null 且它的值具有較佳分佈。</span><span class="sxs-lookup"><span data-stu-id="91555-122">A good way toodetermine if your tables are optimized for export is toorun **DBCC SHOW_STATISTICS** and make sure that hello *RANGE_HI_KEY* is not null and its value has good distribution.</span></span> <span data-ttu-id="91555-123">如需詳細資料，請參閱 [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx)。</span><span class="sxs-lookup"><span data-stu-id="91555-123">For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="91555-124">Bacpac 不預期的 toobe 用於備份和還原作業。</span><span class="sxs-lookup"><span data-stu-id="91555-124">BACPACs are not intended toobe used for backup and restore operations.</span></span> <span data-ttu-id="91555-125">Azure SQL Database 會自動為每個使用者資料庫建立備份。</span><span class="sxs-lookup"><span data-stu-id="91555-125">Azure SQL Database automatically creates backups for every user database.</span></span> <span data-ttu-id="91555-126">如需詳細資訊，請參閱[商務持續性概觀](sql-database-business-continuity.md)和 [SQL Database 備份](sql-database-automated-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="91555-126">For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).</span></span>  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a><span data-ttu-id="91555-127">使用 Azure 入口網站 hello tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="91555-127">Export tooa BACPAC file using hello Azure portal</span></span>

<span data-ttu-id="91555-128">資料庫使用 tooexport hello [Azure 入口網站](https://portal.azure.com)，開啟資料庫的 hello 頁面，按一下 **匯出**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="91555-128">tooexport a database using hello [Azure portal](https://portal.azure.com), open hello page for your database and click **Export** on hello toolbar.</span></span> <span data-ttu-id="91555-129">指定 hello BACPAC 檔案名稱、 提供 hello Azure 儲存體帳戶和容器 hello 匯出，並提供 hello 認證 tooconnect toohello 來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="91555-129">Specify hello BACPAC filename, provide hello Azure storage account and container for hello export, and provide hello credentials tooconnect toohello source database.</span></span>  

![資料庫匯出](./media/sql-database-export/database-export.png)

<span data-ttu-id="91555-131">hello toomonitor hello 進度匯出作業中，開啟 hello 邏輯伺服器包含 hello 資料庫正在匯出的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="91555-131">toomonitor hello progress of hello export operation, open hello page for hello logical server containing hello database being exported.</span></span> <span data-ttu-id="91555-132">向下捲動太**作業**，然後按一下**匯入/匯出**歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="91555-132">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

<span data-ttu-id="91555-133">![匯出記錄](./media/sql-database-export/export-history.png)
![匯出記錄狀態](./media/sql-database-export/export-history2.png)</span><span class="sxs-lookup"><span data-stu-id="91555-133">![export history](./media/sql-database-export/export-history.png)
![export history status](./media/sql-database-export/export-history2.png)</span></span>

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a><span data-ttu-id="91555-134">使用 hello SQLPackage 公用程式 tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="91555-134">Export tooa BACPAC file using hello SQLPackage utility</span></span>

<span data-ttu-id="91555-135">tooexport SQL 資料庫使用 hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx)命令列公用程式，請參閱[匯出參數和屬性](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties)。</span><span class="sxs-lookup"><span data-stu-id="91555-135">tooexport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties).</span></span> <span data-ttu-id="91555-136">hello SQLPackage 公用程式隨附的 hello 最新版[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)和[SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)，或者，您可以下載 hello 最新版本的[SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)直接 hello Microsoft 下載中心。</span><span class="sxs-lookup"><span data-stu-id="91555-136">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="91555-137">我們建議 hello 用於 hello SQLPackage 公用程式的規模和效能，在大部分的實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="91555-137">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="91555-138">SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="91555-138">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="91555-139">這個範例會示範如何 tooexport SqlPackage.exe 使用 Active Directory 通用驗證的資料庫：</span><span class="sxs-lookup"><span data-stu-id="91555-139">This example shows how tooexport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a><span data-ttu-id="91555-140">使用 SQL Server Management Studio (SSMS) tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="91555-140">Export tooa BACPAC file using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="91555-141">hello 最新版本的 SQL Server Management Studio 也提供精靈 tooexport Azure SQL Database tooa BACPAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="91555-141">hello newest versions of SQL Server Management Studio also provide a wizard tooexport an Azure SQL Database tooa BACPAC file.</span></span> <span data-ttu-id="91555-142">請參閱 hello[匯出資料層應用程式](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)。</span><span class="sxs-lookup"><span data-stu-id="91555-142">See hello [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).</span></span>

## <a name="export-tooa-bacpac-file-using-powershell"></a><span data-ttu-id="91555-143">使用 PowerShell tooa BACPAC 檔案匯出</span><span class="sxs-lookup"><span data-stu-id="91555-143">Export tooa BACPAC file using PowerShell</span></span>

<span data-ttu-id="91555-144">使用 hello[新增 AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit 匯出資料庫要求 toohello Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="91555-144">Use hello [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit an export database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="91555-145">根據資料庫的 hello 大小，hello 匯出作業可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="91555-145">Depending on hello size of your database, hello export operation may take some time toocomplete.</span></span>

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

<span data-ttu-id="91555-146">hello toocheck hello 狀態匯出要求，請使用 hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="91555-146">toocheck hello status of hello export request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="91555-147">Hello 後立即執行此要求會通常傳回**狀態： InProgress**。</span><span class="sxs-lookup"><span data-stu-id="91555-147">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="91555-148">當您看到**狀態： 成功**hello 匯出已完成。</span><span class="sxs-lookup"><span data-stu-id="91555-148">When you see **Status: Succeeded** hello export is complete.</span></span>

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a><span data-ttu-id="91555-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91555-149">Next steps</span></span>

* <span data-ttu-id="91555-150">關於 Azure SQL 資料庫做為替代的 tooexported 封存用途的資料庫備份的長期備份保留 toolearn 請參閱[長期備份的保留](sql-database-long-term-retention.md)。</span><span class="sxs-lookup"><span data-stu-id="91555-150">toolearn about long-term backup retention of an Azure SQL database backup as an alternative tooexported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).</span></span>
- <span data-ttu-id="91555-151">SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="91555-151">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="91555-152">toolearn 有關匯入 BACPAC tooa SQL Server 資料庫，請參閱[BACPCAC tooa SQL Server 資料庫匯入](https://msdn.microsoft.com/library/hh710052.aspx)。</span><span class="sxs-lookup"><span data-stu-id="91555-152">toolearn about importing a BACPAC tooa SQL Server database, see [Import a BACPCAC tooa SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).</span></span>
* <span data-ttu-id="91555-153">請參閱有關從 SQL Server 資料庫匯出 BACPAC toolearn[匯出資料層應用程式](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)和[移轉您的第一個資料庫](sql-database-migrate-your-sql-server-database.md)。</span><span class="sxs-lookup"><span data-stu-id="91555-153">toolearn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).</span></span>
* <span data-ttu-id="91555-154">如果您匯出從 SQL Server prelude toomigration tooAzure SQL 資料庫，請參閱[移轉 SQL 資料庫的 SQL Server 資料庫 tooAzure](sql-database-cloud-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="91555-154">If you are exporting from SQL Server as a prelude toomigration tooAzure SQL Database, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>
