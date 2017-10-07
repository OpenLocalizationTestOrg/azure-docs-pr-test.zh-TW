---
title: "aaaManage 的計算能力，在 Azure SQL 資料倉儲 (PowerShell) |Microsoft 文件"
description: "PowerShell 工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>管理 Azure SQL 資料倉儲中的計算能力 (PowerShell)
> [!div class="op_single_selector"]
> * [概觀](sql-data-warehouse-manage-compute-overview.md)
> * [入口網站](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>開始之前
### <a name="install-hello-latest-version-of-azure-powershell"></a>安裝 Azure PowerShell hello 最新版本
> [!NOTE]
> toouse 向 SQL 資料倉儲的 Azure PowerShell，您需要 Azure PowerShell 1.0.3 版或更新版本。  tooverify 您目前的版本執行 hello 命令**Get-module-ListAvailable-Name Azure**。 您可以安裝來自 hello 最新版本[Microsoft Web Platform Installer][Microsoft Web Platform Installer]。  如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell][How tooinstall and configure Azure PowerShell]。
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>開始使用 Azure PowerShell Cmdlet
tooget 啟動：

1. 開啟 Azure PowerShell。
2. Hello PowerShell 命令提示字元，執行這些命令 toosign toohello Azure 資源管理員中，選取您的訂用帳戶。

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>調整計算能力
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello Dwu，使用 hello[組 AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] PowerShell cmdlet。 hello 下列範例會設定 hello 服務等級目標 tooDW1000 hello 資料庫裝載 MySQLDW MyServer 伺服器上。

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>暫停計算
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause 資料庫中，使用 hello[暫停 AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] cmdlet。 hello 下列範例會暫停名為 Database02 裝載於名為 Server01 的伺服器上的資料庫。 hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。

> [!NOTE]
> 請注意，如果您的伺服器是 foo.database.windows.net，做為"foo"hello-ServerName hello PowerShell cmdlet。
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
一種變化中下, 一個範例會將擷取 hello 資料庫到 hello $database 物件。 它接著會使用管線傳送 hello 物件太[暫停 AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]。 hello 結果會儲存在 hello 物件 resultDatabase。 hello 最後一個命令會顯示 hello 結果。

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>繼續計算
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart 資料庫中，使用 hello[繼續 AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] cmdlet。 hello 下列範例會啟動名為 Database02 裝載於名為 Server01 的伺服器上的資料庫。 hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

一種變化中下, 一個範例會將擷取 hello 資料庫到 hello $database 物件。 它接著會使用管線傳送 hello 物件太[繼續 AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase]並儲存在 $resultDatabase hello 結果。 hello 最後一個命令會顯示 hello 結果。

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>檢查資料庫狀態

Hello，上述範例所示，您可以使用[Get AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] cmdlet tooget 資訊在資料庫上，藉此檢查 hello 狀態，但也 toouse 做為引數。 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

這會導致如以下的結果 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

可以再檢查 toosee hello*狀態*的 hello 資料庫。 在此情況下，您會看到此資料庫已上線。 

當您執行此命令時，應該會收到下列其中一個 Status (狀態) 值：Online (上線)、Pausing (暫停中)、Resuming (正在恢復)、Scaling (正在調整) 及 Paused (已暫停)。

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>後續步驟
如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
