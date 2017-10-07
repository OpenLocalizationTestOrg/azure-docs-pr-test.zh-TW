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
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>匯入 BACPAC 檔案 tooa 新的 Azure SQL Database

當您需要 tooimport 從封存資料庫，或從另一個平台移轉時，您可以匯入 hello 資料庫結構描述和資料從[BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)檔案。 BACPAC 檔案是包含 hello 中繼資料和資料從 SQL Server 資料庫的 BACPAC 的延伸模組 ZIP 檔案。 BACPAC 檔案可以從 Azure Blob 儲存體 (僅限標準儲存體) 匯入，或從內部部署位置中的本機儲存體匯入。 toomaximize hello 匯入的速度，我們建議您指定較高服務層和效能層級，P6，例如，並 hello 匯入成功後，再擴充 toodown 適當。 此外，hello 匯入後的 hello 資料庫相容性層級根據 hello hello 來源資料庫的相容性層級。 

> [!IMPORTANT] 
> 移轉您的資料庫 tooAzure SQL 資料庫之後，您可以選擇 toooperate hello 資料庫在其目前的相容性層級 （層級 100 hello AdventureWorks2008R2 資料庫） 或更高的層級。 如需有關 hello 含意與作業系統特定的相容性層級的資料庫選項的詳細資訊，請參閱[ALTER DATABASE 相容性層級](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。 另請參閱[ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)對於其他資料庫層級設定的相關資訊與相關 toocompatibility 層級。   >

> [!NOTE]
> tooimport BACPAC tooa 新的資料庫，您必須先建立 Azure SQL Database 邏輯伺服器。 如需顯示如何 toomigrate SQL Server 資料庫 tooAzure SQL Database 的教學課程使用 SQLPackage，請參閱[移轉 SQL Server 資料庫](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>使用 Azure 入口網站從 BACPAC 檔案匯入

本文章提供指示，說明如何從 Azure blob 儲存體中使用 hello 的 BACPAC 檔案建立 Azure SQL database [Azure 入口網站](https://portal.azure.com)。 匯入使用 hello Azure 入口網站支援從 Azure blob 儲存體匯入 BACPAC 檔案。

資料庫使用 tooimport hello Azure 入口網站、 資料庫和按一下開啟 hello 頁面**匯入**hello 工具列上。 指定 hello 儲存體帳戶和容器，然後選取您想要 tooimport hello BACPAC 檔案。 選取 hello hello 新的資料庫大小 (通常 hello 相同做原點)，並提供 hello 目的地 SQL Server 認證。  

   ![資料庫匯入](./media/sql-database-import/import.png)

hello toomonitor hello 進度匯入作業中，開啟 hello 邏輯伺服器包含 hello 資料庫匯入的 hello 頁面。 向下捲動太**作業**，然後按一下**匯入/匯出**歷程記錄。

### <a name="monitor-hello-progress-of-an-import-operation"></a>匯入作業的監視 hello 進度

hello toomonitor hello 進度匯入作業中，開啟 hello 邏輯伺服器的資料庫正在匯入哪些 hello 匯入的 hello 頁面。 向下捲動太**作業**，然後按一下**匯入/匯出**歷程記錄。
   
   ![匯入](./media/sql-database-import/import-history.png)![匯入狀態](./media/sql-database-import/import-status.png)

tooverify hello 資料庫是即時 hello 伺服器上，按一下  **SQL 資料庫**，並確認新資料庫的 hello**線上**。

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>使用 SQLPackage 從 BACPAC 檔案匯入

tooimport SQL 資料庫使用 hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx)命令列公用程式，請參閱[匯入參數和屬性](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties)。 hello SQLPackage 公用程式隨附的 hello 最新版[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)和[SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)，或者，您可以下載 hello 最新版本的[SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)直接 hello Microsoft 下載中心。

我們建議 hello 用於 hello SQLPackage 公用程式的規模和效能，在大部分的實際執行環境。 SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。

請參閱下列指令碼範例的 SQLPackage 命令 hello tooimport hello **AdventureWorks2008R2**資料庫從本機儲存體 tooan Azure SQL Database 邏輯伺服器，稱為**mynewserver20170403**在此範例中。 此指令碼會顯示 hello 建立新的資料庫稱為**myMigratedDatabase**，服務層的**Premium**，以及服務目標的**P6**。 變更這些值做為適當的 tooyour 環境。

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![sqlpackage 匯入](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Azure SQL Database 邏輯伺服器會接聽連接埠 1433。 如果您正嘗試 tooconnect tooan Azure SQL Database 邏輯伺服器從公司防火牆內，此連接埠必須在 hello 公司防火牆中開啟您 toosuccessfully 連線。
>

這個範例會示範如何 tooimport SqlPackage.exe 使用 Active Directory 通用驗證的資料庫：

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>使用 PowerShell 從 BACPAC 檔案匯入

使用 hello[新增 AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit 匯入資料庫要求 toohello Azure SQL Database 服務。 根據資料庫的 hello 大小，hello 匯入作業可能需要一些時間 toocomplete。

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

hello toocheck hello 狀態匯入要求，請使用 hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet。 Hello 後立即執行此要求會通常傳回**狀態： InProgress**。 當您看到**狀態： 成功**hello 匯入作業完成。

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
如需其他指令碼範例，請參閱[從 BACPAC 檔案匯入資料庫](scripts/sql-database-import-from-bacpac-powershell.md)。

## <a name="next-steps"></a>後續步驟
* toolearn 如何 tooconnect tooand 查詢匯入的 SQL 資料庫，請參閱[連接 SQL Server Management Studio tooSQL 資料庫及執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)。
* SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。
* 如需 hello 整個 SQL Server 資料庫移轉程序，包括效能建議的討論，請參閱[移轉 SQL 資料庫的 SQL Server 資料庫 tooAzure](sql-database-cloud-migrate.md)。



