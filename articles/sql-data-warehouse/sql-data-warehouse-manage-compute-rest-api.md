---
title: "在 Azure SQL 資料倉儲中暫停、繼續、使用 REST 調整 | Microsoft Docs"
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
ms.openlocfilehash: 24e43205c0c562fca9b1c2c0e5eed4da54e17ed7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="92793-103">管理 Azure SQL 資料倉儲中的計算能力 (REST)</span><span class="sxs-lookup"><span data-stu-id="92793-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="92793-104">概觀</span><span class="sxs-lookup"><span data-stu-id="92793-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="92793-105">入口網站</span><span class="sxs-lookup"><span data-stu-id="92793-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="92793-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92793-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="92793-107">REST</span><span class="sxs-lookup"><span data-stu-id="92793-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="92793-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="92793-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="92793-109">調整計算能力</span><span class="sxs-lookup"><span data-stu-id="92793-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="92793-110">若要變更 DWU，請使用[建立或更新資料庫][Create or Update Database] REST API。</span><span class="sxs-lookup"><span data-stu-id="92793-110">To change the DWUs, use the [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="92793-111">下例會將裝載在 MyServer 伺服器上的資料庫 MySQLDW 的服務等級目標設定為 DW1000。</span><span class="sxs-lookup"><span data-stu-id="92793-111">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="92793-112">此伺服器位於 ResourceGroup1 這個 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="92793-112">The server is in an Azure resource group named ResourceGroup1.</span></span>

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

## <a name="pause-compute"></a><span data-ttu-id="92793-113">暫停計算</span><span class="sxs-lookup"><span data-stu-id="92793-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="92793-114">若要暫停資料庫，請使用[暫停資料庫][Pause Database] REST API。</span><span class="sxs-lookup"><span data-stu-id="92793-114">To pause a database, use the [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="92793-115">下例會暫停裝載在 Server01 伺服器上的 Database02 資料庫。</span><span class="sxs-lookup"><span data-stu-id="92793-115">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="92793-116">此伺服器位於 ResourceGroup1 這個 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="92793-116">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="92793-117">繼續計算</span><span class="sxs-lookup"><span data-stu-id="92793-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="92793-118">若要啟動資料庫，請使用[繼續資料庫][Resume Database] REST API。</span><span class="sxs-lookup"><span data-stu-id="92793-118">To start a database, use the [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="92793-119">下例會啟動裝載在 Server01 伺服器上的 Database02 資料庫。</span><span class="sxs-lookup"><span data-stu-id="92793-119">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="92793-120">此伺服器位於 ResourceGroup1 這個 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="92793-120">The server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="92793-121">檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="92793-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="92793-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92793-122">Next steps</span></span>
<span data-ttu-id="92793-123">如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="92793-123">For other management tasks, see [Management overview][Management overview].</span></span>

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
