---
title: "還原 Azure SQL 資料倉儲 (PowerShell) | Microsoft Docs"
description: "還原 Azure SQL 資料倉儲的 PowerShell 工作。"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jenniehubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 12/06/2017
ms.author: barbkess
ms.openlocfilehash: 3b39e87946f3787c71872c7b98db419f1f239e7a
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>還原 Azure SQL 資料倉儲 (PowerShell)
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [入口網站][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

在本文中，您將了解如何使用 PowerShell 來還原 Azure SQL 資料倉儲。

## <a name="before-you-begin"></a>開始之前
**請驗證您的 DTU 容量。** 每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。  在您還原 SQL 資料倉儲之前，請確認您的 SQL 伺服器有足夠的剩餘 DTU 配額供要還原的資料庫使用。 若要了解如何計算所需 DTU 或要求更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。

### <a name="install-powershell"></a>安裝 PowerShell
若要搭配使用 Azure Powershell 與 SQL 資料倉儲，您需要安裝 Azure PowerShell 1.0 版或更高版本。  您可以執行 **Get-Module -ListAvailable -Name AzureRM**來檢查您的版本。  可透過 [Microsoft Web Platform Installer][Microsoft Web Platform Installer]安裝最新的版本。  如需安裝最新版本的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell][How to install and configure Azure PowerShell]。

## <a name="restore-an-active-or-paused-database"></a>還原作用中或已暫停的資料庫
若要從快照還原資料庫，請使用 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell Cmdlet。

1. 開啟 Windows PowerShell。
2. 連接到您的 Azure 帳戶，然後列出與您帳戶關聯的所有訂用帳戶。
3. 選取包含要還原之資料庫的訂用帳戶。
4. 列出資料庫的還原點。
5. 使用 RestorePointCreationDate 挑選出想要的還原點。
6. 將資料庫還原到想要的還原點。
7. 確認還原的資料庫在線上。

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName)).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> 還原完成後，您可以遵循[在復原之後設定資料庫][Configure your database after recovery]來設定復原的資料庫。
> 
> 

## <a name="restore-a-deleted-database"></a>還原已刪除的資料庫
若要還原已刪除的資料庫，請使用 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] Cmdlet。

1. 開啟 Windows PowerShell。
2. 連接到您的 Azure 帳戶，然後列出與您帳戶關聯的所有訂用帳戶。
3. 選取包含要還原之已刪除資料庫的訂用帳戶。
4. 取得已刪除的特定資料庫。
5. 還原已刪除的資料庫。
6. 確認還原的資料庫在線上。

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> 還原完成後，您可以遵循[在復原之後設定資料庫][Configure your database after recovery]來設定復原的資料庫。
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>從 Azure 地理區域還原
若要還原資料庫，請使用 [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] Cmdlet。

1. 開啟 Windows PowerShell。
2. 連接到您的 Azure 帳戶，然後列出與您帳戶關聯的所有訂用帳戶。
3. 選取包含要還原之資料庫的訂用帳戶。
4. 取得您想要復原的資料庫。
5. 建立資料庫的復原要求。
6. 確認異地還原資料庫的狀態。

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> 若要在還原完成之後設定資料庫，請參閱[在復原之後設定資料庫][Configure your database after recovery]。
> 
> 

如果來源資料庫是啟用 TDE，則復原的資料庫將是啟用 TDE。

## <a name="next-steps"></a>後續步驟
若要深入了解 Azure SQL Database 版本的商務持續性功能，請閱讀 [Azure SQL Database 商務持續性概觀][Azure SQL Database business continuity overview]。

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
