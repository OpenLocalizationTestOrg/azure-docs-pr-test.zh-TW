---
title: "T-SQL：管理 Azure SQL Database 彈性集區 | Microsoft Docs"
description: "使用 T-SQL 管理 Azure SQL Database 彈性集區。"
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: c6b64e4a7fd91283a37a792b294965064d653003
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="0f40d-103">使用 Transact-SQL 監視和管理彈性集區</span><span class="sxs-lookup"><span data-stu-id="0f40d-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="0f40d-104">本主題說明如何使用 Transact-SQL 管理可調整的[彈性集區](sql-database-elastic-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="0f40d-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="0f40d-105">您也可以使用 [Azure 入口網站](https://portal.azure.com/)、[PowerShell](sql-database-elastic-pool-manage-powershell.md)、REST API 或 [C#](sql-database-elastic-pool-manage-csharp.md) 來建立及管理 Azure 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="0f40d-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="0f40d-106">您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="0f40d-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="0f40d-107">使用 [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) 和 [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) 命令建立資料庫，以及將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="0f40d-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="0f40d-108">必須先有彈性集區，您才可以使用這些命令。</span><span class="sxs-lookup"><span data-stu-id="0f40d-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="0f40d-109">這些命令只會影響資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f40d-109">These commands affect only databases.</span></span> <span data-ttu-id="0f40d-110">無法使用 T-SQL 命令來變更新集區的建立和集區屬性 (例如最小和最大 Edtu) 的設定。</span><span class="sxs-lookup"><span data-stu-id="0f40d-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="0f40d-111">在彈性集區中建立集區資料庫</span><span class="sxs-lookup"><span data-stu-id="0f40d-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="0f40d-112">使用 CREATE DATABASE 命令搭配 SERVICE_OBJECTIVE 選項。</span><span class="sxs-lookup"><span data-stu-id="0f40d-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="0f40d-113">彈性集區中的所有資料庫都會都繼承彈性集區的服務層 (基本、標準、進階)。</span><span class="sxs-lookup"><span data-stu-id="0f40d-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="0f40d-114">在彈性集區之間移動資料庫</span><span class="sxs-lookup"><span data-stu-id="0f40d-114">Move a database between elastic pools</span></span>
<span data-ttu-id="0f40d-115">使用 ALTER DATABASE 命令搭配 MODIFY，並將 SERVICE\_OBJECTIVE 選項設定為 ELASTIC\_POOL。</span><span class="sxs-lookup"><span data-stu-id="0f40d-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="0f40d-116">將名稱設定為目標集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f40d-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="0f40d-117">將資料庫移入彈性集區</span><span class="sxs-lookup"><span data-stu-id="0f40d-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="0f40d-118">使用 ALTER DATABASE 命令搭配 MODIFY，並將 SERVICE\_OBJECTIVE 選項設定為 ELASTIC_POOL。</span><span class="sxs-lookup"><span data-stu-id="0f40d-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="0f40d-119">將名稱設定為目標集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="0f40d-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="0f40d-120">將資料庫移出彈性集區</span><span class="sxs-lookup"><span data-stu-id="0f40d-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="0f40d-121">使用 ALTER DATABASE 命令並將 SERVICE_OBJECTIVE 設定為其中一個效能層級 (如 S0 或 S1)。</span><span class="sxs-lookup"><span data-stu-id="0f40d-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="0f40d-122">列出彈性集區中的資料庫</span><span class="sxs-lookup"><span data-stu-id="0f40d-122">List databases in an elastic pool</span></span>
<span data-ttu-id="0f40d-123">使用 [sys.database\_service\_objectives view](https://msdn.microsoft.com/library/mt712619)列出彈性集區中的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f40d-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="0f40d-124">登入 master 資料庫來查詢檢視。</span><span class="sxs-lookup"><span data-stu-id="0f40d-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="0f40d-125">取得彈性集區的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="0f40d-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="0f40d-126">使用 [sys.elastic\_pool\_resource\_stats view](https://msdn.microsoft.com/library/mt280062.aspx)來檢查邏輯伺服器上彈性集區的資源使用量統計資料。</span><span class="sxs-lookup"><span data-stu-id="0f40d-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="0f40d-127">登入 master 資料庫來查詢檢視。</span><span class="sxs-lookup"><span data-stu-id="0f40d-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="0f40d-128">取得集區資料庫的資源使用量</span><span class="sxs-lookup"><span data-stu-id="0f40d-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="0f40d-129">使用 [sys.dm\_ db\_resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) 或 [sys.resource\_stats view](https://msdn.microsoft.com/library/dn269979.aspx) 來檢查彈性集區中資料庫的資源使用量統計資料。</span><span class="sxs-lookup"><span data-stu-id="0f40d-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="0f40d-130">此程序類似於查詢單一資料庫的資源使用量。</span><span class="sxs-lookup"><span data-stu-id="0f40d-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f40d-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f40d-131">Next steps</span></span>
<span data-ttu-id="0f40d-132">建立彈性集區後，可以藉由建立彈性工作來管理集區中的彈性資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f40d-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="0f40d-133">彈性工作有助於對集區中任意數目的資料庫執行 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0f40d-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="0f40d-134">如需詳細資訊，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0f40d-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="0f40d-135">請參閱[使用 Azure SQL Database 相應放大](sql-database-elastic-scale-introduction.md)︰使用彈性資料庫工具相應放大、移動資料、查詢或建立交易。</span><span class="sxs-lookup"><span data-stu-id="0f40d-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

