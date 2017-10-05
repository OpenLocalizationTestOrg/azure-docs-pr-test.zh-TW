---
title: "在 Azure SQL 資料倉儲中暫停、繼續、使用 T-SQL 調整 | Microsoft Docs"
description: "透過調整 DWU 以相應放大效能的 Transact-SQL (T-SQL) 工作。 透過在非尖峰時間進行縮減以節省成本。"
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
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="2d44d-104">管理 Azure SQL 資料倉儲中的計算能力 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="2d44d-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d44d-105">概觀</span><span class="sxs-lookup"><span data-stu-id="2d44d-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="2d44d-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="2d44d-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="2d44d-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d44d-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="2d44d-108">REST</span><span class="sxs-lookup"><span data-stu-id="2d44d-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="2d44d-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="2d44d-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="2d44d-110">檢視目前的 DWU 設定</span><span class="sxs-lookup"><span data-stu-id="2d44d-110">View current DWU settings</span></span>
<span data-ttu-id="2d44d-111">若要檢視您的資料庫的目前 DWU 設定︰</span><span class="sxs-lookup"><span data-stu-id="2d44d-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="2d44d-112">在 Visual Studio 中開啟 [SQL Server 物件總管]。</span><span class="sxs-lookup"><span data-stu-id="2d44d-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="2d44d-113">連接到與邏輯 SQL Database 伺服器相關聯的 master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d44d-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="2d44d-114">從 sys.database_service_objectives 動態管理檢視中選取。</span><span class="sxs-lookup"><span data-stu-id="2d44d-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="2d44d-115">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="2d44d-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="2d44d-116">調整計算</span><span class="sxs-lookup"><span data-stu-id="2d44d-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="2d44d-117">若要變更 DWU︰</span><span class="sxs-lookup"><span data-stu-id="2d44d-117">To change the DWUs:</span></span>

1. <span data-ttu-id="2d44d-118">連接到與您的邏輯 SQL Database 伺服器相關聯的 master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d44d-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="2d44d-119">使用 [ALTER DATABASE][ALTER DATABASE] TSQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="2d44d-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="2d44d-120">下例範例會將資料庫 MySQLDW 的服務等級目標設定為 DW1000。</span><span class="sxs-lookup"><span data-stu-id="2d44d-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="2d44d-121">檢查資料庫狀態和作業進度</span><span class="sxs-lookup"><span data-stu-id="2d44d-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="2d44d-122">連接到與您的邏輯 SQL Database 伺服器相關聯的 master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2d44d-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="2d44d-123">送出查詢以檢查資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="2d44d-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="2d44d-124">送出查詢以檢查作業的狀態</span><span class="sxs-lookup"><span data-stu-id="2d44d-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="2d44d-125">此 DMV 會傳回您「SQL 資料倉儲」上各種管理作業的相關資訊，例如作業和作業的狀態 (不是 IN_PROGRESS 就是 COMPLETED)。</span><span class="sxs-lookup"><span data-stu-id="2d44d-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="2d44d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d44d-126">Next steps</span></span>
<span data-ttu-id="2d44d-127">如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="2d44d-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
