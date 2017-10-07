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
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Azure SQL database tooa BACPAC 檔案匯出

當您需要 tooexport 資料庫，為了封存或移動 tooanother 平台時，您可以匯出 hello 資料庫結構描述和資料 tooa [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4)檔案。 BACPAC 檔案是包含 hello 中繼資料和資料從 SQL Server 資料庫的 BACPAC 的延伸模組 ZIP 檔案。 BACPAC 檔案可以儲存在 Azure Blob 儲存體，或在內部部署位置的本機儲存體中，之後再匯入至 Azure SQL Database 或 SQL Server 內部部署安裝。 

> [!IMPORTANT] 
> Azure SQL Database 自動匯出已在 2017 年 3 月 1 日淘汰。 您可以使用[長期備份的保留](sql-database-long-term-retention.md
)或[Azure 自動化](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md)tooperiodically 封存的 SQL 資料庫使用 PowerShell，根據您選擇的 tooa 排程。 如需範例，請下載 hello[範例 PowerShell 指令碼](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export)從 Github。
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>匯出 Azure SQL Database 時的考量

* 匯出 toobe 具有交易一致性，您必須確定任一 hello 在匯出期間，正在發生之任何寫入活動，或者您要匯出從[交易一致性複本](sql-database-copy.md)您的 Azure SQL database。
* 如果您正在匯出 tooblob 儲存體，hello BACPAC 檔案的大小上限為 200 GB。 tooarchive 較大的 BACPAC 檔案匯出 toolocal 儲存體。
* 不支援匯出 BACPAC 檔案 tooAzure 高階儲存體使用本文所討論的 hello 方法。
* 如果從 Azure SQL Database 的 hello 匯出作業超過 20 小時，它可能會取消。 在匯出期間 tooincrease 效能，您可以：
  * 暫時提高您的服務等級。
  * 停止所有讀取及寫入 hello 匯出期間的活動。
  * 在所有大型資料表上搭配使用 [叢集索引](https://msdn.microsoft.com/library/ms190457.aspx) 和非 null 值。 若沒有叢集索引，如果要花超過 6-12 小時，匯出可能會失敗。 這是因為 hello 匯出服務需要 toocomplete 資料表掃描 tootry tooexport 整個資料表。 如果匯出為 toorun 最佳化資料表的好方法 toodetermine **DBCC SHOW_STATISTICS** ，並確定該 hello *RANGE_HI_KEY*不是 null 且它的值具有較佳分佈。 如需詳細資料，請參閱 [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx)。

> [!NOTE]
> Bacpac 不預期的 toobe 用於備份和還原作業。 Azure SQL Database 會自動為每個使用者資料庫建立備份。 如需詳細資訊，請參閱[商務持續性概觀](sql-database-business-continuity.md)和 [SQL Database 備份](sql-database-automated-backups.md)。  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>使用 Azure 入口網站 hello tooa BACPAC 檔案匯出

資料庫使用 tooexport hello [Azure 入口網站](https://portal.azure.com)，開啟資料庫的 hello 頁面，按一下 **匯出**hello 工具列上。 指定 hello BACPAC 檔案名稱、 提供 hello Azure 儲存體帳戶和容器 hello 匯出，並提供 hello 認證 tooconnect toohello 來源資料庫。  

![資料庫匯出](./media/sql-database-export/database-export.png)

hello toomonitor hello 進度匯出作業中，開啟 hello 邏輯伺服器包含 hello 資料庫正在匯出的 hello 頁面。 向下捲動太**作業**，然後按一下**匯入/匯出**歷程記錄。

![匯出記錄](./media/sql-database-export/export-history.png)
![匯出記錄狀態](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>使用 hello SQLPackage 公用程式 tooa BACPAC 檔案匯出

tooexport SQL 資料庫使用 hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx)命令列公用程式，請參閱[匯出參數和屬性](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties)。 hello SQLPackage 公用程式隨附的 hello 最新版[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)和[SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx)，或者，您可以下載 hello 最新版本的[SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876)直接 hello Microsoft 下載中心。

我們建議 hello 用於 hello SQLPackage 公用程式的規模和效能，在大部分的實際執行環境。 SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。

這個範例會示範如何 tooexport SqlPackage.exe 使用 Active Directory 通用驗證的資料庫：

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) tooa BACPAC 檔案匯出

hello 最新版本的 SQL Server Management Studio 也提供精靈 tooexport Azure SQL Database tooa BACPAC 檔案。 請參閱 hello[匯出資料層應用程式](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)。

## <a name="export-tooa-bacpac-file-using-powershell"></a>使用 PowerShell tooa BACPAC 檔案匯出

使用 hello[新增 AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) cmdlet toosubmit 匯出資料庫要求 toohello Azure SQL Database 服務。 根據資料庫的 hello 大小，hello 匯出作業可能需要一些時間 toocomplete。

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

hello toocheck hello 狀態匯出要求，請使用 hello [Get AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet。 Hello 後立即執行此要求會通常傳回**狀態： InProgress**。 當您看到**狀態： 成功**hello 匯出已完成。

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

## <a name="next-steps"></a>後續步驟

* 關於 Azure SQL 資料庫做為替代的 tooexported 封存用途的資料庫備份的長期備份保留 toolearn 請參閱[長期備份的保留](sql-database-long-term-retention.md)。
- SQL Server 客戶諮詢團隊部落格有關移轉使用 BACPAC 檔案，請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。
* toolearn 有關匯入 BACPAC tooa SQL Server 資料庫，請參閱[BACPCAC tooa SQL Server 資料庫匯入](https://msdn.microsoft.com/library/hh710052.aspx)。
* 請參閱有關從 SQL Server 資料庫匯出 BACPAC toolearn[匯出資料層應用程式](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application)和[移轉您的第一個資料庫](sql-database-migrate-your-sql-server-database.md)。
* 如果您匯出從 SQL Server prelude toomigration tooAzure SQL 資料庫，請參閱[移轉 SQL 資料庫的 SQL Server 資料庫 tooAzure](sql-database-cloud-migrate.md)。
