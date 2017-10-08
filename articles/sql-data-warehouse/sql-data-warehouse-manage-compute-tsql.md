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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="ac4ba-104">管理 Azure SQL 資料倉儲中的計算能力 (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="ac4ba-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac4ba-105">概觀</span><span class="sxs-lookup"><span data-stu-id="ac4ba-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="ac4ba-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="ac4ba-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="ac4ba-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac4ba-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="ac4ba-108">REST</span><span class="sxs-lookup"><span data-stu-id="ac4ba-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="ac4ba-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="ac4ba-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="ac4ba-110">檢視目前的 DWU 設定</span><span class="sxs-lookup"><span data-stu-id="ac4ba-110">View current DWU settings</span></span>
<span data-ttu-id="ac4ba-111">tooview hello 目前的 DWU 設定您的資料庫：</span><span class="sxs-lookup"><span data-stu-id="ac4ba-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="ac4ba-112">在 Visual Studio 中開啟 [SQL Server 物件總管]。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="ac4ba-113">連接 toohello hello 邏輯 SQL Database 伺服器相關聯的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="ac4ba-114">選取從 hello sys.database_service_objectives 動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="ac4ba-115">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="ac4ba-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="ac4ba-116">調整計算</span><span class="sxs-lookup"><span data-stu-id="ac4ba-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="ac4ba-117">toochange hello dwu 調整：</span><span class="sxs-lookup"><span data-stu-id="ac4ba-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="ac4ba-118">連接邏輯的 SQL Database 伺服器相關聯的 toohello master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="ac4ba-119">使用 hello [ALTER DATABASE] [ ALTER DATABASE] TSQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="ac4ba-120">hello 下列範例會設定 hello 服務等級目標 tooDW1000 hello 資料庫 MySQLDW。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="ac4ba-121">檢查資料庫狀態和作業進度</span><span class="sxs-lookup"><span data-stu-id="ac4ba-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="ac4ba-122">連接邏輯的 SQL Database 伺服器相關聯的 toohello master 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="ac4ba-123">提交查詢 toocheck 資料庫狀態</span><span class="sxs-lookup"><span data-stu-id="ac4ba-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="ac4ba-124">提交作業的查詢 toocheck 狀態</span><span class="sxs-lookup"><span data-stu-id="ac4ba-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="ac4ba-125">此 DMV 會傳回您的 SQL 資料倉儲，例如 hello hello 作業將會是 IN_PROGRESS 或完成的作業和 hello 狀態上的各種管理操作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="ac4ba-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac4ba-126">Next steps</span></span>
<span data-ttu-id="ac4ba-127">如需其他管理工作的詳細資訊，請參閱[管理概觀][Management overview]。</span><span class="sxs-lookup"><span data-stu-id="ac4ba-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
