---
title: "匯入 BACPAC 檔案以建立 Azure SQL Database | Microsoft Docs"
description: "匯入 BACPAC 檔案以建立新的 Azure SQL Database。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 285e17ed6d0ce700cb518864df7a3b5f5e55bee5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="import-a-bacpac-file-to-a-new-azure-sql-database"></a><span data-ttu-id="badfe-103">將 BACPAC 檔案匯入到新的 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="badfe-103">Import a BACPAC file to a new Azure SQL Database</span></span>

<span data-ttu-id="badfe-104">當您需要從封存匯入資料庫或從另一個平台進行移轉時，您可以從 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 檔案匯入資料庫結構描述和資料。</span><span class="sxs-lookup"><span data-stu-id="badfe-104">When you need to import a database from an archive or when migrating from another platform, you can import the database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="badfe-105">BACPAC 檔案是一種副檔名為 BACPAC 的 ZIP 檔案，其包含來自 SQL Server Database 的中繼資料和資料。</span><span class="sxs-lookup"><span data-stu-id="badfe-105">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="badfe-106">BACPAC 檔案可以從 Azure Blob 儲存體 (僅限標準儲存體) 匯入，或從內部部署位置中的本機儲存體匯入。</span><span class="sxs-lookup"><span data-stu-id="badfe-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="badfe-107">若要使匯入速度最大化，我們建議您指定較高的服務層和效能等級 (例如 P6)，然後在匯入成功後，適當地向下調整。</span><span class="sxs-lookup"><span data-stu-id="badfe-107">To maximize the import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale to down as appropriate after the import is successful.</span></span> <span data-ttu-id="badfe-108">此外，匯入之後的資料庫相容性等級會以來源資料庫的相容性等級為基礎。</span><span class="sxs-lookup"><span data-stu-id="badfe-108">Also, the database compatibility level after the import is based on the compatibility level of the source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="badfe-109">您將資料庫移轉至 Azure SQL Database 後，可選擇於目前的相容性等級 (針對 AdventureWorks2008R2 資料庫為等級 100) 或更高等級運作資料庫。</span><span class="sxs-lookup"><span data-stu-id="badfe-109">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="badfe-110">如需於特定相容性層級操作資料庫的含意與選項詳細資訊，請參閱 [ALTER DATABASE 相容性層級 (ALTER DATABASE Compatibility Level)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。</span><span class="sxs-lookup"><span data-stu-id="badfe-110">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="badfe-111">如需相容性層級其他相關資料庫等級設定的資訊，另請參閱 [ALTER DATABASE 範圍組態 (ALTER DATABASE SCOPED CONFIGURATION)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)。</span><span class="sxs-lookup"><span data-stu-id="badfe-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="badfe-112">若要將 BACPAC 匯入到新的資料庫，您必須先建立 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="badfe-112">To import a BACPAC to a new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="badfe-113">如需如何使用 SQLPackage 將 SQL Server Database 移轉到 Azure SQL Database 的教學課程，請參閱[移轉 SQL Server 資料庫](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="badfe-113">For a tutorial showing you how to migrate a SQL Server database to Azure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="badfe-114">使用 Azure 入口網站從 BACPAC 檔案匯入</span><span class="sxs-lookup"><span data-stu-id="badfe-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="badfe-115">本文提供的指示將說明如何使用 [Azure 入口網站](https://portal.azure.com)，從 BACPAC 檔案 (儲存於 Azure Blob 儲存體中) 建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="badfe-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="badfe-116">使用 Azure 入口網站匯入的方式只支援從 Azure Blob 儲存體匯入 BACPAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="badfe-116">Import using the Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="badfe-117">若要使用 Azure 入口網站匯入資料庫，請開啟資料庫頁面，然後按一下工具列上的 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="badfe-117">To import a database using the Azure portal, open the page for your database and click **Import** on the toolbar.</span></span> <span data-ttu-id="badfe-118">指定儲存體帳戶和容器，然後選取您要匯入的 BACPAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="badfe-118">Specify the storage account and container, and select the BACPAC file you want to import.</span></span> <span data-ttu-id="badfe-119">選取新資料庫的大小 (通常與來源相同)，並提供目的地 SQL Server 認證。</span><span class="sxs-lookup"><span data-stu-id="badfe-119">Select the size of the new database (usually the same as origin) and provide the destination SQL Server credentials.</span></span>  

   ![資料庫匯入](./media/sql-database-import/import.png)

<span data-ttu-id="badfe-121">若要監視匯入作業的進度，請開啟包含匯入資料庫的邏輯伺服器頁面。</span><span class="sxs-lookup"><span data-stu-id="badfe-121">To monitor the progress of the import operation, open the page for the logical server containing the database being imported.</span></span> <span data-ttu-id="badfe-122">向下捲動至**作業**，然後按一下 [匯入/匯出歷程記錄] 。</span><span class="sxs-lookup"><span data-stu-id="badfe-122">Scroll down to **Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-the-progress-of-an-import-operation"></a><span data-ttu-id="badfe-123">監視匯入作業的進度</span><span class="sxs-lookup"><span data-stu-id="badfe-123">Monitor the progress of an import operation</span></span>

<span data-ttu-id="badfe-124">若要監視匯入作業的進度，請將邏輯伺服器的頁面開啟為要匯入的資料庫。</span><span class="sxs-lookup"><span data-stu-id="badfe-124">To monitor the progress of the import operation, open the page for the logical server into which the database is being imported imported.</span></span> <span data-ttu-id="badfe-125">向下捲動至**作業**，然後按一下 [匯入/匯出歷程記錄] 。</span><span class="sxs-lookup"><span data-stu-id="badfe-125">Scroll down to **Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="badfe-126">![匯入](./media/sql-database-import/import-history.png)![匯入狀態](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="badfe-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="badfe-127">確認伺服器上的資料庫為線上狀態，請按一下 [SQL 資料庫]，並確認新的資料庫為 [線上]。</span><span class="sxs-lookup"><span data-stu-id="badfe-127">To verify the database is live on the server, click **SQL databases** and verify the new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="badfe-128">使用 SQLPackage 從 BACPAC 檔案匯入</span><span class="sxs-lookup"><span data-stu-id="badfe-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="badfe-129">若要使用 [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) 命令列公用程式匯入 SQL Database，請參閱[匯入參數和屬性](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties)。</span><span class="sxs-lookup"><span data-stu-id="badfe-129">To import a SQL database using the [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="badfe-130">SQLPackage 公用程式隨附於最新版的 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)，或者您也可以直接從 Microsoft 下載中心下載最新版的 [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)。</span><span class="sxs-lookup"><span data-stu-id="badfe-130">The SQLPackage utility ships with the latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download the latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from the Microsoft download center.</span></span>

<span data-ttu-id="badfe-131">針對大部分生產環境中的延展性和效能，我們建議您使用 SQLPackage 公用程式。</span><span class="sxs-lookup"><span data-stu-id="badfe-131">We recommend the use of the SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="badfe-132">如需 SQL Server 客戶諮詢小組部落格中有關使用 BACPAC 檔案進行移轉的主題，請參閱[使用 BACPAC 檔案從 SQL Server 移轉至 Azure SQL Database](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="badfe-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="badfe-133">請參閱下列 SQLPackage 命令，以取得如何將 **AdventureWorks2008R2** 資料庫從本機儲存體匯入到 Azure SQL Database 邏輯伺服器 (在此範例中稱為 **mynewserver20170403**) 的指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="badfe-133">See the following SQLPackage command for a script example for how to import the **AdventureWorks2008R2** database from local storage to an Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="badfe-134">此指令碼會示範如何建立名為 **myMigratedDatabase** 的新資料庫，並搭配 **Premium (進階)**服務層和 **P6** 服務目標。</span><span class="sxs-lookup"><span data-stu-id="badfe-134">This script shows the creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="badfe-135">將這些值變更為適合您環境的值。</span><span class="sxs-lookup"><span data-stu-id="badfe-135">Change these values as appropriate to your environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage 匯入](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="badfe-137">Azure SQL Database 邏輯伺服器會接聽連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="badfe-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="badfe-138">如果您嘗試從公司防火牆連線至 Azure SQL Database 邏輯伺服器，則必須在公司防火牆中開啟此連接埠，您才能成功連線。</span><span class="sxs-lookup"><span data-stu-id="badfe-138">If you are attempting to connect to an Azure SQL Database logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

<span data-ttu-id="badfe-139">此範例會說明如何透過 Active Directory 通用驗證使用 SqlPackage.exe 匯入資料庫：</span><span class="sxs-lookup"><span data-stu-id="badfe-139">This example shows how to import a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="badfe-140">使用 PowerShell 從 BACPAC 檔案匯入</span><span class="sxs-lookup"><span data-stu-id="badfe-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="badfe-141">使用 [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) Cmdlet 來提交匯入資料庫要求至 Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="badfe-141">Use the [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet to submit an import database request to the Azure SQL Database service.</span></span> <span data-ttu-id="badfe-142">視資料庫大小而定，匯入作業可能需要一些時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="badfe-142">Depending on the size of your database, the import operation may take some time to complete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="badfe-143">若要查看匯入要求的狀態，請使用 [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="badfe-143">To check the status of the import request, use the [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="badfe-144">如果在要求後立即執行此 Cmdlet，通常會傳回 **Status : InProgress**。</span><span class="sxs-lookup"><span data-stu-id="badfe-144">Running this immediately after the request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="badfe-145">當您看見 **Status: Succeeded** 時，便代表匯入已完成。</span><span class="sxs-lookup"><span data-stu-id="badfe-145">When you see **Status: Succeeded** the import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="badfe-146">如需其他指令碼範例，請參閱[從 BACPAC 檔案匯入資料庫](scripts/sql-database-import-from-bacpac-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="badfe-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="badfe-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="badfe-147">Next steps</span></span>
* <span data-ttu-id="badfe-148">若要了解如何連接並查詢匯入的 SQL Database，請參閱[使用 SQL Server Management Studio 連接到 SQL Database 並執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="badfe-148">To learn how to connect to and query an imported SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="badfe-149">如需 SQL Server 客戶諮詢小組部落格中有關使用 BACPAC 檔案進行移轉的主題，請參閱[使用 BACPAC 檔案從 SQL Server 移轉至 Azure SQL Database](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="badfe-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="badfe-150">如需有關整個 SQL Server 資料庫移轉程序的討論，包括效能建議，請參閱[將 SQL Server 資料庫移轉至 Azure SQL Database](sql-database-cloud-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="badfe-150">For a discussion of the entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database to Azure SQL Database](sql-database-cloud-migrate.md).</span></span>



