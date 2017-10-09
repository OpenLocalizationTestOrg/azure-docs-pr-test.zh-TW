---
title: "aaaCreate SQL 資料倉儲與 TSQL |Microsoft 文件"
description: "了解如何 toocreate Azure SQL 資料倉儲與 TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>使用 Transact-SQL (TSQL) 建立 SQL 資料倉儲資料庫
> [!div class="op_single_selector"]
> * [Azure 入口網站](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

本文章將示範如何 toocreate SQL 資料倉儲使用 T-SQL。

## <a name="prerequisites"></a>必要條件
tooget 開始，您需要：

* **Azure 帳戶**： 瀏覽[Azure 免費試用][ Azure Free Trial]或[MSDN Azure 信用額度][ MSDN Azure Credits] toocreate 帳戶。
* **Azure SQL server**： 請參閱 [建立 hello Azure 入口網站的 Azure SQL Database 邏輯伺服器] [以 hello Azure 入口網站建立 Azure SQL Database 邏輯伺服器] 或 [使用 PowerShell 建立 Azure SQL Database 邏輯伺服器] [建立 Azure SQL使用 PowerShell 邏輯伺服器的資料庫] 如需詳細資訊。
* **資源群組**： 請使用相同的資源與您的 Azure SQL server 群組，或參閱的 hello[如何 toocreate 資源群組][how toocreate a resource group]。
* **環境 tooexecute T-SQL**： 您可以使用[Visual Studio][Installing Visual Studio and SSDT]， [sqlcmd][sqlcmd]，或[SSMS][ SSMS] tooexecute T-SQL。

> [!NOTE]
> 建立 SQL 資料倉儲可能會導致新的可計費服務。  如需價格的詳細資訊，請參閱 [SQL 資料倉儲價格][SQL Data Warehouse pricing]。
>
>

## <a name="create-a-database-with-visual-studio"></a>使用 Visual Studio 建立資料庫
如果您是新 tooVisual Studio，請參閱 hello 文章[查詢 Azure SQL 資料倉儲 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]。  toostart，Visual Studio 中開啟 SQL Server 物件總管，並將裝載 SQL 資料倉儲資料庫 toohello 伺服器連線。  一旦連接之後，您可以建立 SQL 資料倉儲由執行下列 SQL 命令，針對 hello hello**主要**資料庫。  此命令會建立 hello 資料庫 MySqlDwDb DW400 服務目標，並允許 hello 資料庫 toogrow tooa 最大大小的 10 TB。

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>使用 sqlcmd 建立資料庫
或者，您可以執行下列的命令提示字元的同一個命令使用 sqlcmd 執行 hello 的 hello。

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

hello 預設定序時未指定為定序 SQL_Latin1_General_CP1_CI_AS。  hello`MAXSIZE`可以是 250 GB 到 240 TB 之間。  hello`SERVICE_OBJECTIVE`可介於 DW100 到 DW2000 [DWU][DWU]。  如需所有有效的值的清單，請參閱 hello MSDN 文件[CREATE DATABASE][CREATE DATABASE]。  Hello MAXSIZE 和 SERVICE_OBJECTIVE 來將其變更與[ALTER DATABASE] [ ALTER DATABASE] T-SQL 命令。  建立之後就無法變更資料庫定序 hello。   變更為變更 DWU hello service_objective，將會導致重新啟動服務，這樣會取消航班中的所有查詢時，應注意。  變更 MAXSIZE 並不會重新啟動服務，因為這只是簡單的中繼資料作業。

## <a name="next-steps"></a>後續步驟
您可以佈建完成您的 SQL 資料倉儲後[範例資料載入][ load sample data]或太簽出如何[開發][develop]， [載入][load]，或[移轉][migrate]。

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
