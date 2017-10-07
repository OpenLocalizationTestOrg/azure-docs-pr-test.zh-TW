---
title: "T-SQL：管理 Azure SQL Database 彈性集區 | Microsoft Docs"
description: "使用 T-SQL toomanage Azure SQL Database 彈性集區。"
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
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="44e66-103">使用 Transact-SQL 監視和管理彈性集區</span><span class="sxs-lookup"><span data-stu-id="44e66-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="44e66-104">本主題說明如何 toomanage 可擴充[彈性集區](sql-database-elastic-pool.md)使用 Transact SQL。</span><span class="sxs-lookup"><span data-stu-id="44e66-104">This topic shows you how toomanage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="44e66-105">您也可以建立和管理 Azure 的彈性集區 hello [Azure 入口網站](https://portal.azure.com/)， [PowerShell](sql-database-elastic-pool-manage-powershell.md)，hello REST API 或[C#](sql-database-elastic-pool-manage-csharp.md)。</span><span class="sxs-lookup"><span data-stu-id="44e66-105">You can also create and manage an Azure elastic pool hello [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="44e66-106">您也可以使用 [Transact-SQL](sql-database-elastic-pool-manage-tsql.md) 來建立資料庫並將它移入和移出彈性集區。</span><span class="sxs-lookup"><span data-stu-id="44e66-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="44e66-107">使用 hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx)和[Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx)彈性集區進出命令 toocreate 和移動資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e66-107">Use hello [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands toocreate and move databases into and out of elastic pools.</span></span> <span data-ttu-id="44e66-108">您可以使用這些命令之前，必須存在 hello 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="44e66-108">hello elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="44e66-109">這些命令只會影響資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e66-109">These commands affect only databases.</span></span> <span data-ttu-id="44e66-110">建立新的集區及 hello 設定 （例如 min 和 max Edtu) 的集區屬性無法變更使用 T-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="44e66-110">Creation of new pools and hello setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="44e66-111">在彈性集區中建立集區資料庫</span><span class="sxs-lookup"><span data-stu-id="44e66-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="44e66-112">使用 hello CREATE DATABASE 命令和 hello SERVICE_OBJECTIVE 選項。</span><span class="sxs-lookup"><span data-stu-id="44e66-112">Use hello CREATE DATABASE command with hello SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="44e66-113">彈性集區中的所有資料庫都會都繼承 hello 彈性集區 （Basic、 Standard、 Premium） 的 hello 服務層。</span><span class="sxs-lookup"><span data-stu-id="44e66-113">All databases in an elastic pool inherit hello service tier of hello elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="44e66-114">在彈性集區之間移動資料庫</span><span class="sxs-lookup"><span data-stu-id="44e66-114">Move a database between elastic pools</span></span>
<span data-ttu-id="44e66-115">以 hello 修改使用 hello ALTER DATABASE 命令，並設定服務\_目標選項設定為彈性\_集區。</span><span class="sxs-lookup"><span data-stu-id="44e66-115">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="44e66-116">設定 hello 名稱 toohello hello 目標集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="44e66-116">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="44e66-117">將資料庫移入彈性集區</span><span class="sxs-lookup"><span data-stu-id="44e66-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="44e66-118">以 hello 修改使用 hello ALTER DATABASE 命令，並設定服務\_ELASTIC_POOL 為目標的選項。</span><span class="sxs-lookup"><span data-stu-id="44e66-118">Use hello ALTER DATABASE command with hello MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="44e66-119">設定 hello 名稱 toohello hello 目標集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="44e66-119">Set hello name toohello name of hello target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="44e66-120">將資料庫移出彈性集區</span><span class="sxs-lookup"><span data-stu-id="44e66-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="44e66-121">使用 hello ALTER DATABASE 命令，並設定 hello SERVICE_OBJECTIVE tooone hello 效能層級 （例如 S0 或 S1）。</span><span class="sxs-lookup"><span data-stu-id="44e66-121">Use hello ALTER DATABASE command and set hello SERVICE_OBJECTIVE tooone of hello performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="44e66-122">列出彈性集區中的資料庫</span><span class="sxs-lookup"><span data-stu-id="44e66-122">List databases in an elastic pool</span></span>
<span data-ttu-id="44e66-123">使用 hello [log_reuse_wait_desc\_服務\_目標檢視](https://msdn.microsoft.com/library/mt712619)toolist 所有 hello 彈性集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e66-123">Use hello [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) toolist all hello databases in an elastic pool.</span></span> <span data-ttu-id="44e66-124">登入 toohello master 資料庫 tooquery hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="44e66-124">Log in toohello master database tooquery hello view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="44e66-125">取得彈性集區的資源使用量資料</span><span class="sxs-lookup"><span data-stu-id="44e66-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="44e66-126">使用 hello [sys.elastic\_集區\_資源\_統計檢視](https://msdn.microsoft.com/library/mt280062.aspx)tooexamine hello 資源使用量統計資料的邏輯伺服器上彈性集區。</span><span class="sxs-lookup"><span data-stu-id="44e66-126">Use hello [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="44e66-127">登入 toohello master 資料庫 tooquery hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="44e66-127">Log in toohello master database tooquery hello view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="44e66-128">取得集區資料庫的資源使用量</span><span class="sxs-lookup"><span data-stu-id="44e66-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="44e66-129">使用 hello [sys.dm\_ db\_資源\_統計檢視](https://msdn.microsoft.com/library/dn800981.aspx)或[sys.resource\_統計檢視](https://msdn.microsoft.com/library/dn269979.aspx)tooexamine hello 資源使用量統計資料的彈性集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e66-129">Use hello [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) tooexamine hello resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="44e66-130">此程序是單一資料庫的類似 tooquerying 資源使用量。</span><span class="sxs-lookup"><span data-stu-id="44e66-130">This process is similar tooquerying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e66-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44e66-131">Next steps</span></span>
<span data-ttu-id="44e66-132">在建立之後彈性集區，您可以藉由建立彈性的工作管理 hello 集區中的彈性資料庫。</span><span class="sxs-lookup"><span data-stu-id="44e66-132">After creating an elastic pool, you can manage elastic databases in hello pool by creating elastic jobs.</span></span> <span data-ttu-id="44e66-133">彈性的作業有助於針對任意數目的 hello 集區中的資料庫執行 T-SQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="44e66-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in hello pool.</span></span> <span data-ttu-id="44e66-134">如需詳細資訊，請參閱 [彈性資料庫工作概觀](sql-database-elastic-jobs-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="44e66-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="44e66-135">請參閱[使用 Azure SQL Database 向外延展](sql-database-elastic-scale-introduction.md)： 使用彈性資料庫工具 tooscale 外的，移動資料、 查詢或建立的交易。</span><span class="sxs-lookup"><span data-stu-id="44e66-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools tooscale out, move data, query, or create transactions.</span></span>

