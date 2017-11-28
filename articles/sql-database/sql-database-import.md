---
title: "aaaImport BACPAC 檔案的 Azure SQL database toocreate |Microsoft 文件"
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
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="b17d6-103">匯入 BACPAC 檔案 tooa 新的 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="b17d6-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="b17d6-104">當您需要 tooimport 從封存資料庫，或從另一個平台移轉時，您可以匯入 hello 資料庫結構描述和資料從[BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)檔案。</span><span class="sxs-lookup"><span data-stu-id="b17d6-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="b17d6-105">BACPAC 檔案是包含 hello 中繼資料和資料從 SQL Server 資料庫的 BACPAC 的延伸模組 ZIP 檔案。</span><span class="sxs-lookup"><span data-stu-id="b17d6-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="b17d6-106">BACPAC 檔案可以從 Azure Blob 儲存體 (僅限標準儲存體) 匯入，或從內部部署位置中的本機儲存體匯入。</span><span class="sxs-lookup"><span data-stu-id="b17d6-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="b17d6-107">toomaximize hello 匯入的速度，我們建議您指定較高服務層和效能層級，P6，例如，並 hello 匯入成功後，再擴充 toodown 適當。</span><span class="sxs-lookup"><span data-stu-id="b17d6-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="b17d6-108">此外，hello 匯入後的 hello 資料庫相容性層級根據 hello hello 來源資料庫的相容性層級。</span><span class="sxs-lookup"><span data-stu-id="b17d6-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="b17d6-109">移轉您的資料庫 tooAzure SQL 資料庫之後，您可以選擇 toooperate hello 資料庫在其目前的相容性層級 （層級 100 hello AdventureWorks2008R2 資料庫） 或更高的層級。</span><span class="sxs-lookup"><span data-stu-id="b17d6-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="b17d6-110">如需有關 hello 含意與作業系統特定的相容性層級的資料庫選項的詳細資訊，請參閱[ALTER DATABASE 相容性層級](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="b17d6-111">另請參閱[ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)對於其他資料庫層級設定的相關資訊與相關 toocompatibility 層級。</span><span class="sxs-lookup"><span data-stu-id="b17d6-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="b17d6-112">tooimport BACPAC tooa 新的資料庫，您必須先建立 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="b17d6-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="b17d6-113">如需顯示如何 toomigrate SQL Server 資料庫 tooAzure SQL Database 的教學課程使用 SQLPackage，請參閱[移轉 SQL Server 資料庫](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="b17d6-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="b17d6-114">使用 Azure 入口網站從 BACPAC 檔案匯入</span><span class="sxs-lookup"><span data-stu-id="b17d6-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="b17d6-115">本文章提供指示，說明如何從 Azure blob 儲存體中使用 hello 的 BACPAC 檔案建立 Azure SQL database [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b17d6-116">匯入使用 hello Azure 入口網站支援從 Azure blob 儲存體匯入 BACPAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="b17d6-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="b17d6-117">資料庫使用 tooimport hello Azure 入口網站、 資料庫和按一下開啟 hello 頁面**匯入**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="b17d6-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="b17d6-118">指定 hello 儲存體帳戶和容器，然後選取您想要 tooimport hello BACPAC 檔案。</span><span class="sxs-lookup"><span data-stu-id="b17d6-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="b17d6-119">選取 hello hello 新的資料庫大小 (通常 hello 相同做原點)，並提供 hello 目的地 SQL Server 認證。</span><span class="sxs-lookup"><span data-stu-id="b17d6-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![資料庫匯入](./media/sql-database-import/import.png)

<span data-ttu-id="b17d6-121">hello toomonitor hello 進度匯入作業中，開啟 hello 邏輯伺服器包含 hello 資料庫匯入的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="b17d6-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="b17d6-122">向下捲動太**作業**，然後按一下**匯入/匯出**歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="b17d6-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="b17d6-123">匯入作業的監視 hello 進度</span><span class="sxs-lookup"><span data-stu-id="b17d6-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="b17d6-124">hello toomonitor hello 進度匯入作業中，開啟 hello 邏輯伺服器的資料庫正在匯入哪些 hello 匯入的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="b17d6-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="b17d6-125">向下捲動太**作業**，然後按一下**匯入/匯出**歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="b17d6-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="b17d6-126">![匯入](./media/sql-database-import/import-history.png)![匯入狀態](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="b17d6-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="b17d6-127">tooverify hello 資料庫是即時 hello 伺服器上，按一下  **SQL 資料庫**，並確認新資料庫的 hello**線上**。</span><span class="sxs-lookup"><span data-stu-id="b17d6-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="b17d6-128">使用 SQLPackage 從 BACPAC 檔案匯入</span><span class="sxs-lookup"><span data-stu-id="b17d6-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="b17d6-129">tooimport SQL 資料庫使用 hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx)命令列公用程式，請參閱[匯入參數和屬性](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="b17d6-130">hello SQLPackage 公用程式隨附的 hello 最新版[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)和[SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)，或者，您可以下載 hello 最新版本的[SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)直接 hello Microsoft 下載中心。</span><span class="sxs-lookup"><span data-stu-id="b17d6-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="b17d6-131">我們建議 hello 用於 hello SQLPackage 公用程式的規模和效能，在大部分的實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="b17d6-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="b17d6-132">SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="b17d6-133">請參閱下列指令碼範例的 SQLPackage 命令 hello tooimport hello **AdventureWorks2008R2**資料庫從本機儲存體 tooan Azure SQL Database 邏輯伺服器，稱為**mynewserver20170403**在此範例中。</span><span class="sxs-lookup"><span data-stu-id="b17d6-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="b17d6-134">此指令碼會顯示 hello 建立新的資料庫稱為**myMigratedDatabase**，服務層的**Premium**，以及服務目標的**P6**。</span><span class="sxs-lookup"><span data-stu-id="b17d6-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="b17d6-135">變更這些值做為適當的 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="b17d6-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage 匯入](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="b17d6-137">Azure SQL Database 邏輯伺服器會接聽連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="b17d6-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="b17d6-138">如果您正嘗試 tooconnect tooan Azure SQL Database 邏輯伺服器從公司防火牆內，此連接埠必須在 hello 公司防火牆中開啟您 toosuccessfully 連線。</span><span class="sxs-lookup"><span data-stu-id="b17d6-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="b17d6-139">這個範例會示範如何 tooimport SqlPackage.exe 使用 Active Directory 通用驗證的資料庫：</span><span class="sxs-lookup"><span data-stu-id="b17d6-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="b17d6-140">使用 PowerShell 從 BACPAC 檔案匯入</span><span class="sxs-lookup"><span data-stu-id="b17d6-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="b17d6-141">使用 hello[新增 AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit 匯入資料庫要求 toohello Azure SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="b17d6-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="b17d6-142">根據資料庫的 hello 大小，hello 匯入作業可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b17d6-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

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

<span data-ttu-id="b17d6-143">hello toocheck hello 狀態匯入要求，請使用 hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b17d6-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="b17d6-144">Hello 後立即執行此要求會通常傳回**狀態： InProgress**。</span><span class="sxs-lookup"><span data-stu-id="b17d6-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="b17d6-145">當您看到**狀態： 成功**hello 匯入作業完成。</span><span class="sxs-lookup"><span data-stu-id="b17d6-145">When you see **Status: Succeeded** hello import is complete.</span></span>

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
<span data-ttu-id="b17d6-146">如需其他指令碼範例，請參閱[從 BACPAC 檔案匯入資料庫](scripts/sql-database-import-from-bacpac-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b17d6-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b17d6-147">Next steps</span></span>
* <span data-ttu-id="b17d6-148">toolearn 如何 tooconnect tooand 查詢匯入的 SQL 資料庫，請參閱[連接 SQL Server Management Studio tooSQL 資料庫及執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="b17d6-149">SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="b17d6-150">如需 hello 整個 SQL Server 資料庫移轉程序，包括效能建議的討論，請參閱[移轉 SQL 資料庫的 SQL Server 資料庫 tooAzure](sql-database-cloud-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="b17d6-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



