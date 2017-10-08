---
title: "aaaPause，繼續，請利用 Azure SQL 資料倉儲中的 T-SQL 調整 |Microsoft 文件"
description: "藉由調整 Dwu TRANSACT-SQL (T-SQL) 工作 tooscale 外延展效能。 透過在非尖峰時間進行縮減以節省成本。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>管理 Azure SQL 資料倉儲中的計算能力 (T-SQL)
> [!div class="op_single_selector"]
> * [概觀](sql-data-warehouse-manage-compute-overview.md)
> * [入口網站](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>檢視目前的 DWU 設定
tooview hello 目前的 DWU 設定您的資料庫：

1. 在 Visual Studio 中開啟 [SQL Server 物件總管]。
2. 連接 toohello hello 邏輯 SQL Database 伺服器相關聯的主要資料庫。
3. 選取從 hello sys.database_service_objectives 動態管理檢視。 下列是一個範例： 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>調整計算
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello dwu 調整：

1. 連接邏輯的 SQL Database 伺服器相關聯的 toohello master 資料庫。
2. 使用 hello [ALTER DATABASE] [ ALTER DATABASE] TSQL 陳述式。 hello 下列範例會設定 hello 服務等級目標 tooDW1000 hello 資料庫 MySQLDW。 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>檢查資料庫狀態和作業進度

1. 連接邏輯的 SQL Database 伺服器相關聯的 toohello master 資料庫。
2. 提交查詢 toocheck 資料庫狀態

```sql
SELECT *
FROM
sys.databases
```

3. 提交作業的查詢 toocheck 狀態

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

此 DMV 會傳回您的 SQL 資料倉儲，例如 hello hello 作業將會是 IN_PROGRESS 或完成的作業和 hello 狀態上的各種管理操作的相關資訊。



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>後續步驟
如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
