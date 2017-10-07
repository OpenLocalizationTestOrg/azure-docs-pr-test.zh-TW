---
title: "aaaRestore Azure SQL 資料倉儲 (PowerShell) |Microsoft 文件"
description: "還原 Azure SQL 資料倉儲的 PowerShell 工作。"
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>還原 Azure SQL 資料倉儲 (PowerShell)
> [!div class="op_single_selector"]
> * [概觀][Overview]
> * [入口網站][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

在本文中，您將學習如何 toorestore Azure SQL 資料倉儲使用 PowerShell。

## <a name="before-you-begin"></a>開始之前
**請驗證您的 DTU 容量。** 每個 SQL 資料倉儲均由具有預設 DTU 配額的 SQL 伺服器裝載 (例如 myserver.database.windows.net)。  您可以還原 SQL 資料倉儲之前，請確認您的 SQL server 有足夠的剩餘 hello 要還原的資料庫的 DTU 配額該 hello。 toolearn toocalculate DTU 的所需或 toorequest 更多 DTU，請參閱[要求 DTU 配額變更][Request a DTU quota change]。

### <a name="install-powershell"></a>安裝 PowerShell
在順序 toouse 向 SQL 資料倉儲的 Azure PowerShell，您必須 tooinstall 版本的 Azure PowerShell 1.0 或更新版本。  您可以執行 **Get-Module -ListAvailable -Name AzureRM**來檢查您的版本。  hello 最新版本可以從安裝[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。  如需有關如何安裝 hello 最新版本的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。

## <a name="restore-an-active-or-paused-database"></a>還原作用中或已暫停的資料庫
toorestore 從快照集資料庫使用 hello[還原 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell cmdlet。

1. 開啟 Windows PowerShell。
2. 連接 tooyour Azure 帳戶，然後列出與您的帳戶相關聯的所有 hello 訂閱。
3. 選取包含還原 hello 資料庫 toobe hello 訂用帳戶。
4. 清單 hello 的還原點 hello 資料庫。
5. 挑選使用 hello RestorePointCreationDate hello 需要還原點。
6. 還原 hello 資料庫所需的 toohello 還原點。
7. 請確認該 hello 還原資料庫在線上。

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> Hello 還原完成之後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。
> 
> 

## <a name="restore-a-deleted-database"></a>還原已刪除的資料庫
toorestore 已刪除的資料庫，使用 hello[還原 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet。

1. 開啟 Windows PowerShell。
2. 連接 tooyour Azure 帳戶，然後列出與您的帳戶相關聯的所有 hello 訂閱。
3. 選取包含還原刪除的 hello 資料庫 toobe hello 訂用帳戶。
4. 取得 hello 刪除特定資料庫。
5. 還原 hello 刪除資料庫。
6. 請確認該 hello 還原資料庫在線上。

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> Hello 還原完成之後，您可以依照下列設定復原的資料庫[設定您的資料庫復原後][Configure your database after recovery]。
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>從 Azure 地理區域還原
toorecover 資料庫中，使用 hello[還原 AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet。

1. 開啟 Windows PowerShell。
2. 連接 tooyour Azure 帳戶，然後列出與您的帳戶相關聯的所有 hello 訂閱。
3. 選取包含還原 hello 資料庫 toobe hello 訂用帳戶。
4. 取得您想要的 hello 資料庫 toorecover。
5. 建立 hello hello 資料庫復原要求。
6. 確認 hello hello 異地還原的資料庫狀態。

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> tooconfigure 資料庫之後 hello 還原完成後，請參閱[設定您的資料庫復原後][Configure your database after recovery]。
> 
> 

hello 復原的資料庫會啟用 TDE hello 來源資料庫是啟用 TDE。

## <a name="next-steps"></a>後續步驟
toolearn 有關 hello 業務續航力功能的 Azure SQL Database 的版本，請閱讀 hello [Azure SQL Database 業務持續性概觀][Azure SQL Database business continuity overview]。

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
