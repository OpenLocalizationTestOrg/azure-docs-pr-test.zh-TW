---
title: "aaaPause，繼續，請調整與 Azure SQL 資料倉儲中的其餘部分 |Microsoft 文件"
description: "透過 REST、T-SQL 和 PowerShell 管理 SQL 資料倉儲中的運算能力。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a>管理 Azure SQL 資料倉儲中的計算能力 (REST)
> [!div class="op_single_selector"]
> * [概觀](sql-data-warehouse-manage-compute-overview.md)
> * [入口網站](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>調整計算能力
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello Dwu，使用 hello[建立或更新資料庫][ Create or Update Database] REST API。 hello 下列範例會設定 hello 服務等級目標 tooDW1000 hello 資料庫裝載 MySQLDW MyServer 伺服器上。 hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>暫停計算
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause 資料庫中，使用 hello[暫停資料庫][ Pause Database] REST API。 hello 下列範例會暫停名為 Database02 裝載於名為 Server01 的伺服器上的資料庫。 hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>繼續計算
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart 資料庫中，使用 hello[繼續資料庫][ Resume Database] REST API。 hello 下列範例會啟動名為 Database02 裝載於名為 Server01 的伺服器上的資料庫。 hello 伺服器中的 Azure 資源群組的名稱為 ResourceGroup1。 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a>檢查資料庫狀態

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>後續步驟
如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
