---
title: "將 Azure SQL 資料庫匯出到 BACPAC 檔案 | Microsoft Docs"
description: "使用 Azure 入口網站將 Azure SQL Database 匯出到 BACPAC 檔案"
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
ms.openlocfilehash: faa567ec615a07da8633629fc98e3454c84a8f5f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="export-an-azure-sql-database-to-a-bacpac-file"></a><span data-ttu-id="471b4-103">將 Azure SQL 資料庫匯出到 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="471b4-103">Export an Azure SQL database to a BACPAC file</span></span>

<span data-ttu-id="471b4-104">當您需要匯出資料庫以封存或移至另一個平台時，可以將資料庫結構描述和資料匯出至 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 檔案。</span><span class="sxs-lookup"><span data-stu-id="471b4-104">When you need to export a database for archiving or for moving to another platform, you can export the database schema and data to a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="471b4-105">BACPAC 檔案是一種副檔名為 BACPAC 的 ZIP 檔案，其包含來自 SQL Server Database 的中繼資料和資料。</span><span class="sxs-lookup"><span data-stu-id="471b4-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="471b4-106">BACPAC 檔案可以儲存在 Azure Blob 儲存體，或在內部部署位置的本機儲存體中，之後再匯入至 Azure SQL Database 或 SQL Server 內部部署安裝。</span><span class="sxs-lookup"><span data-stu-id="471b4-106">A BACPAC file can be stored in Azure blob storage or in local storage in an on-premises location and later imported back into Azure SQL Database or into a SQL Server on-premises installation.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="471b4-107">Azure SQL Database 自動匯出已在 2017 年 3 月 1 日淘汰。</span><span class="sxs-lookup"><span data-stu-id="471b4-107">Azure SQL Database Automated Export was retired on March 1, 2017.</span></span> <span data-ttu-id="471b4-108">您可以使用[長期的備份保留](sql-database-long-term-retention.md
)或 [Azure 自動化](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md)，根據您選擇的排程使用 PowerShell 定期封存 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="471b4-108">You can use [long-term backup retention](sql-database-long-term-retention.md
) or [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) to periodically archive SQL databases using PowerShell according to a schedule of your choice.</span></span> <span data-ttu-id="471b4-109">如需範例，請從 Github 下載[範例 PowerShell 指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)。</span><span class="sxs-lookup"><span data-stu-id="471b4-109">For a sample, download the [sample PowerShell script](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) from Github.</span></span>
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a><span data-ttu-id="471b4-110">匯出 Azure SQL Database 時的考量</span><span class="sxs-lookup"><span data-stu-id="471b4-110">Considerations when exporting an Azure SQL database</span></span>

* <span data-ttu-id="471b4-111">為了讓匯出處於交易一致狀態，您必須確定在匯出期間未發生任何寫入活動，或者是從 Azure SQL 資料庫的[交易一致性複本](sql-database-copy.md)匯出。</span><span class="sxs-lookup"><span data-stu-id="471b4-111">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export, or that you are exporting from a [transactionally consistent copy](sql-database-copy.md) of your Azure SQL database.</span></span>
* <span data-ttu-id="471b4-112">如果您要匯出至 blob 儲存體，BACPAC 檔案的大小上限為 200 GB。</span><span class="sxs-lookup"><span data-stu-id="471b4-112">If you are exporting to blob storage, the maximum size of a BACPAC file is 200 GB.</span></span> <span data-ttu-id="471b4-113">若要封存較大的 BACPAC 檔案，請將匯出到本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="471b4-113">To archive a larger BACPAC file, export to local storage.</span></span>
* <span data-ttu-id="471b4-114">不支援使用本文所討論的方法將 BACPAC 檔案匯出到 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="471b4-114">Exporting a BACPAC file to Azure premium storage using the methods discussed in this article is not supported.</span></span>
* <span data-ttu-id="471b4-115">如果執行從 Azure SQL Database 匯出的作業超過 20 個小時，它可能會被取消。</span><span class="sxs-lookup"><span data-stu-id="471b4-115">If the export operation from Azure SQL Database exceeds 20 hours, it may be canceled.</span></span> <span data-ttu-id="471b4-116">若要增加匯出期間的效能，您可以︰</span><span class="sxs-lookup"><span data-stu-id="471b4-116">To increase performance during export, you can:</span></span>
  * <span data-ttu-id="471b4-117">暫時提高您的服務等級。</span><span class="sxs-lookup"><span data-stu-id="471b4-117">Temporarily increase your service level.</span></span>
  * <span data-ttu-id="471b4-118">在匯出期間停止所有讀取及寫入活動。</span><span class="sxs-lookup"><span data-stu-id="471b4-118">Cease all read and write activity during the export.</span></span>
  * <span data-ttu-id="471b4-119">在所有大型資料表上搭配使用 [叢集索引](https://msdn.microsoft.com/library/ms190457.aspx) 和非 null 值。</span><span class="sxs-lookup"><span data-stu-id="471b4-119">Use a [clustered index](https://msdn.microsoft.com/library/ms190457.aspx) with non-null values on all large tables.</span></span> <span data-ttu-id="471b4-120">若沒有叢集索引，如果要花超過 6-12 小時，匯出可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="471b4-120">Without clustered indexes, an export may fail if it takes longer than 6-12 hours.</span></span> <span data-ttu-id="471b4-121">這是因為匯出服務需要完成資料表掃描，以便嘗試匯出整份資料表。</span><span class="sxs-lookup"><span data-stu-id="471b4-121">This is because the export service needs to complete a table scan to try to export entire table.</span></span> <span data-ttu-id="471b4-122">有一個可判斷資料表是否已針對匯出進行最佳化的好方法，就是執行 **DBCC SHOW_STATISTICS**，並確定 *RANGE_HI_KEY* 不是 null 且其值具有良好的分佈。</span><span class="sxs-lookup"><span data-stu-id="471b4-122">A good way to determine if your tables are optimized for export is to run **DBCC SHOW_STATISTICS** and make sure that the *RANGE_HI_KEY* is not null and its value has good distribution.</span></span> <span data-ttu-id="471b4-123">如需詳細資料，請參閱 [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx)。</span><span class="sxs-lookup"><span data-stu-id="471b4-123">For details, see [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="471b4-124">BACPAC 並非用於備份和還原作業。</span><span class="sxs-lookup"><span data-stu-id="471b4-124">BACPACs are not intended to be used for backup and restore operations.</span></span> <span data-ttu-id="471b4-125">Azure SQL Database 會自動為每個使用者資料庫建立備份。</span><span class="sxs-lookup"><span data-stu-id="471b4-125">Azure SQL Database automatically creates backups for every user database.</span></span> <span data-ttu-id="471b4-126">如需詳細資訊，請參閱[商務持續性概觀](sql-database-business-continuity.md)和 [SQL Database 備份](sql-database-automated-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="471b4-126">For details, see [Business Continuity Overview](sql-database-business-continuity.md) and [SQL Database backups](sql-database-automated-backups.md).</span></span>  
> 

## <a name="export-to-a-bacpac-file-using-the-azure-portal"></a><span data-ttu-id="471b4-127">使用 Azure 入口網站匯出到 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="471b4-127">Export to a BACPAC file using the Azure portal</span></span>

<span data-ttu-id="471b4-128">若要使用 [Azure 入口網站](https://portal.azure.com)匯出資料庫，請開啟資料庫頁面，然後按一下工具列上的 [匯出]。</span><span class="sxs-lookup"><span data-stu-id="471b4-128">To export a database using the [Azure portal](https://portal.azure.com), open the page for your database and click **Export** on the toolbar.</span></span> <span data-ttu-id="471b4-129">指定 BACPAC 檔案名稱，並提供匯出的 Azure 儲存體帳戶和容器，然後提供認證以連線至來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="471b4-129">Specify the BACPAC filename, provide the Azure storage account and container for the export, and provide the credentials to connect to the source database.</span></span>  

![資料庫匯出](./media/sql-database-export/database-export.png)

<span data-ttu-id="471b4-131">若要監視匯出作業的進度，請開啟包含匯出資料庫的邏輯伺服器頁面。</span><span class="sxs-lookup"><span data-stu-id="471b4-131">To monitor the progress of the export operation, open the page for the logical server containing the database being exported.</span></span> <span data-ttu-id="471b4-132">向下捲動至**作業**，然後按一下 [匯入/匯出歷程記錄] 。</span><span class="sxs-lookup"><span data-stu-id="471b4-132">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

<span data-ttu-id="471b4-133">![匯出記錄](./media/sql-database-export/export-history.png)
![匯出記錄狀態](./media/sql-database-export/export-history2.png)</span><span class="sxs-lookup"><span data-stu-id="471b4-133">![export history](./media/sql-database-export/export-history.png)
![export history status](./media/sql-database-export/export-history2.png)</span></span>

## <a name="export-to-a-bacpac-file-using-the-sqlpackage-utility"></a><span data-ttu-id="471b4-134">使用 SQLPackage 公用程式匯出到 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="471b4-134">Export to a BACPAC file using the SQLPackage utility</span></span>

<span data-ttu-id="471b4-135">若要使用 [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 命令列公用程式匯出 SQL 資料庫，請參閱[匯出參數和屬性](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties)。</span><span class="sxs-lookup"><span data-stu-id="471b4-135">To export a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Export parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties).</span></span> <span data-ttu-id="471b4-136">SQLPackage 公用程式隨附於最新版的 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)，或者您也可以直接從 Microsoft 下載中心下載最新版的 [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)。</span><span class="sxs-lookup"><span data-stu-id="471b4-136">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="471b4-137">針對大部分生產環境中的延展性和效能，我們建議您使用 SQLPackage 公用程式。</span><span class="sxs-lookup"><span data-stu-id="471b4-137">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="471b4-138">如需 SQL Server 客戶諮詢小組部落格中有關使用 BACPAC 檔案進行移轉的主題，請參閱[使用 BACPAC 檔案從 SQL Server 移轉至 Azure SQL Database](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="471b4-138">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="471b4-139">此範例會說明如何透過 Active Directory 通用驗證使用 SqlPackage.exe 匯出資料庫：</span><span class="sxs-lookup"><span data-stu-id="471b4-139">This example shows how to export a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-to-a-bacpac-file-using-sql-server-management-studio-ssms"></a><span data-ttu-id="471b4-140">使用 SQL Server Management Studio (SSMS) 匯出到 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="471b4-140">Export to a BACPAC file using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="471b4-141">最新版的 SQL Server Management Studio 也提供精靈協助您將 Azure SQL Database 匯出到 BACPAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="471b4-141">The newest versions of SQL Server Management Studio also provide a wizard to export an Azure SQL Database to a BACPAC file.</span></span> <span data-ttu-id="471b4-142">請參閱[匯出資料層應用程式](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)。</span><span class="sxs-lookup"><span data-stu-id="471b4-142">See the [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).</span></span>

## <a name="export-to-a-bacpac-file-using-powershell"></a><span data-ttu-id="471b4-143">使用 PowerShell 匯出到 BACPAC 檔案</span><span class="sxs-lookup"><span data-stu-id="471b4-143">Export to a BACPAC file using PowerShell</span></span>

<span data-ttu-id="471b4-144">使用 [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) Cmdlet 來提交匯出資料庫要求至 Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="471b4-144">Use the [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet to submit an export database request to the Azure SQL Database service.</span></span> <span data-ttu-id="471b4-145">視資料庫大小而定，匯出作業可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="471b4-145">Depending on the size of your database, the export operation may take some time to complete.</span></span>

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

<span data-ttu-id="471b4-146">若要查看匯出要求的狀態，請使用 [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus)Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="471b4-146">To check the status of the export request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="471b4-147">如果在要求後立即執行此 Cmdlet，通常會傳回 **Status : InProgress**。</span><span class="sxs-lookup"><span data-stu-id="471b4-147">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="471b4-148">當您看見 **Status: Succeeded** 時，便代表匯出已完成。</span><span class="sxs-lookup"><span data-stu-id="471b4-148">When you see **Status: Succeeded** the export is complete.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="471b4-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="471b4-149">Next steps</span></span>

* <span data-ttu-id="471b4-150">若要了解除了匯出的資料庫，還有 Azure SQL Database 備份的長期備份保留也可達到封存目的，請參閱[長期備份保留](sql-database-long-term-retention.md)。</span><span class="sxs-lookup"><span data-stu-id="471b4-150">To learn about long-term backup retention of an Azure SQL database backup as an alternative to exported a database for archive purposes, see [Long-term backup retention](sql-database-long-term-retention.md).</span></span>
- <span data-ttu-id="471b4-151">如需 SQL Server 客戶諮詢小組部落格中有關使用 BACPAC 檔案進行移轉的主題，請參閱[使用 BACPAC 檔案從 SQL Server 移轉至 Azure SQL Database](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="471b4-151">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="471b4-152">若要了解如何將 BACPAC 匯入 SQL Server 資料庫，請參閱 [將 BACPAC 匯入 SQL Server 資料庫](https://msdn.microsoft.com/library/hh710052.aspx)。</span><span class="sxs-lookup"><span data-stu-id="471b4-152">To learn about importing a BACPAC to a SQL Server database, see [Import a BACPCAC to a SQL Server database](https://msdn.microsoft.com/library/hh710052.aspx).</span></span>
* <span data-ttu-id="471b4-153">若要了解如何將 BACPAC 從 SQL Server 資料庫匯出，請參閱[匯出資料層應用程式](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)和[移轉您的第一個資料庫](sql-database-migrate-your-sql-server-database.md)。</span><span class="sxs-lookup"><span data-stu-id="471b4-153">To learn about exporting a BACPAC from a SQL Server database, see [Export a Data-tier Application](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) and [Migrate your first database](sql-database-migrate-your-sql-server-database.md).</span></span>
* <span data-ttu-id="471b4-154">如果您要從 SQL Server 匯出以準備移轉至 Azure SQL Database，請參閱[將 SQL Server 資料庫移轉至 Azure SQL Database](sql-database-cloud-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="471b4-154">If you are exporting from SQL Server as a prelude to migration to Azure SQL Database, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>
