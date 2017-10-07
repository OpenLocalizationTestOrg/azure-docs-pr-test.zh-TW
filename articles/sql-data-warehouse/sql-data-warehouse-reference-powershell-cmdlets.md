---
title: "Azure SQL 資料倉儲的 aaaPowerShell cmdlet"
description: "尋找 Azure SQL 資料倉儲 hello 最上層的 PowerShell 指令程式包括如何 toopause 和繼續資料庫。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>適用於 SQL 資料倉儲的 PowerShell Cmdlet 和 REST API
您可使用 Azure PowerShell Cmdlet 或 REST API 管理許多 SQL 資料倉儲系統管理工作。  以下是如何 toouse PowerShell 命令 tooautomate 您的 SQL 資料倉儲中的一般工作的一些範例。  某些良好的其他範例，請參閱 hello 文章[管理與其餘的延展性][Manage scalability with REST]。

> [!NOTE]
> 順序 toouse 向 SQL 資料倉儲的 Azure PowerShell，在中，您需要 Azure PowerShell 1.0.3 版或更新版本。  您可以執行 **Get-Module -ListAvailable -Name Azure**來檢查您的版本。  hello 最新版本可以從安裝[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。  如需有關如何安裝 hello 最新版本的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>開始使用 Azure PowerShell Cmdlet
1. 開啟 Windows PowerShell。
2. Hello PowerShell 命令提示字元，執行這些命令 toosign toohello Azure 資源管理員中，選取您的訂用帳戶。
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>暫停 SQL 資料倉儲範例
暫停 "Server01" 伺服器上託管的 "Database02" 資料庫。  hello 伺服器是在名為"ResourceGroup1。 「 Azure 資源群組

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
一種變化中，此範例會使用管線傳送 hello 擷取物件太[暫停 AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]。  如此一來，hello 資料庫已暫停。 hello 最後一個命令會顯示 hello 結果。

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>啟動 SQL 資料倉儲範例
繼續 "Server01" 伺服器上託管之 "Database02" 資料庫的作業。 hello 伺服器包含在資源群組中名為"ResourceGroup1。 」

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

一種變化，此範例會從 "ResourceGroup1" 資源群組包含的 "Server01" 伺服器中，擷取 "Database02" 資料庫。 它使用管線傳送 hello 擷取物件太[繼續 AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]。

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> 請注意，如果您的伺服器是 foo.database.windows.net，做為"foo"hello-ServerName hello PowerShell cmdlet。
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>其他支援的 PowerShell Cmdlet
這些 PowerShell Cmdlet 皆由 Azure SQL 資料倉儲所支援。

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>後續步驟
如需更多 PowerShell 範例，請參閱：

* [使用 PowerShell 建立 SQL 資料倉儲][Create a SQL Data Warehouse using PowerShell]
* [資料庫還原][Database restore]

如需可以使用 PowerShell 進行自動化的其他工作，請參閱 [Azure SQL Database Cmdlet][Azure SQL Database Cmdlets]。 請注意，Azure SQL 資料倉儲並沒有支援所有的 Azure SQL Database Cmdlet。  如需可以使用 REST 來自動化的工作清單，請參閱 [Azure SQL Database 的作業][Operations for Azure SQL Databases]。

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
