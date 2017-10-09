---
title: "aaaConfigure 地理複寫的 Azure SQL Database 使用 TRANSACT-SQL |Microsoft 文件"
description: "使用 Transact-SQL 為 Azure SQL Database 設定異地複寫"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="4942b-103">使用 Transact-SQL 為 Azure SQL Database 設定作用中異地複寫</span><span class="sxs-lookup"><span data-stu-id="4942b-103">Configure active geo-replication for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="4942b-104">本文章將示範如何 tooconfigure 的作用中地理複寫使用 Azure SQL Database TRANSACT-SQL。</span><span class="sxs-lookup"><span data-stu-id="4942b-104">This article shows you how tooconfigure active geo-replication for an Azure SQL Database with Transact-SQL.</span></span>

<span data-ttu-id="4942b-105">tooinitiate 容錯移轉使用 TRANSACT-SQL，請參閱[起始已規劃或未規劃的容錯移轉 Azure SQL database 使用 TRANSACT-SQL](sql-database-geo-replication-failover-transact-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="4942b-105">tooinitiate failover using Transact-SQL, see [Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4942b-106">當您使用災害復原的作用中地理複寫 （可讀取次要資料庫），您應該設定應用程式 tooenable 自動和透明容錯移轉的所有資料庫的容錯移轉群組。</span><span class="sxs-lookup"><span data-stu-id="4942b-106">When you use active geo-replication (readable secondaries) for disaster recovery you should configure a failover group for all databases within an application tooenable automatic and transparent failover.</span></span> <span data-ttu-id="4942b-107">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="4942b-107">This feature is in preview.</span></span> <span data-ttu-id="4942b-108">如需詳細資訊，請參閱[自動容錯移轉群組和異地複寫](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4942b-108">For more information see [Auto-failover groups and geo-replication](sql-database-geo-replication-overview.md).</span></span>
> 
> 

<span data-ttu-id="4942b-109">tooconfigure 作用中地理複寫使用 TRANSACT-SQL，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="4942b-109">tooconfigure active geo-replication using Transact-SQL, you need hello following:</span></span>

* <span data-ttu-id="4942b-110">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4942b-110">An Azure subscription</span></span>
* <span data-ttu-id="4942b-111">Azure SQL Database 邏輯伺服器<MyLocalServer>和 SQL database <MyDB> -您想 tooreplicate hello 主要資料庫</span><span class="sxs-lookup"><span data-stu-id="4942b-111">A logical Azure SQL Database server <MyLocalServer> and a SQL database <MyDB> - hello primary database that you want tooreplicate</span></span>
* <span data-ttu-id="4942b-112">一或多個邏輯 Azure SQL Database 伺服器 < MySecondaryServer(n) >-hello 邏輯將會是您要在其中建立次要資料庫的 hello 夥伴伺服器的伺服器</span><span class="sxs-lookup"><span data-stu-id="4942b-112">One or more logical Azure SQL Database servers <MySecondaryServer(n)> - hello logical servers that will be hello partner servers in which you will create secondary databases</span></span>
* <span data-ttu-id="4942b-113">為 DBManager hello 主要的登入</span><span class="sxs-lookup"><span data-stu-id="4942b-113">A login that is DBManager on hello primary</span></span>
* <span data-ttu-id="4942b-114">具有 db_ownership hello 本機資料庫，您會進行異地複寫</span><span class="sxs-lookup"><span data-stu-id="4942b-114">Have db_ownership of hello local database that you will geo-replicate</span></span>
* <span data-ttu-id="4942b-115">DBManager 位於 hello 夥伴伺服器 toowhich 您將設定異地複寫</span><span class="sxs-lookup"><span data-stu-id="4942b-115">Be DBManager on hello partner server(s) toowhich you will configure geo-replication</span></span>
* <span data-ttu-id="4942b-116">hello 最新版本的 SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="4942b-116">hello newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4942b-117">建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4942b-117">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="4942b-118">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4942b-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

## <a name="add-secondary-database"></a><span data-ttu-id="4942b-119">加入次要資料庫</span><span class="sxs-lookup"><span data-stu-id="4942b-119">Add secondary database</span></span>
<span data-ttu-id="4942b-120">您可以使用 hello **ALTER DATABASE**陳述式 toocreate 夥伴伺服器上，進行地理複寫的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-120">You can use hello **ALTER DATABASE** statement toocreate a geo-replicated secondary database on a partner server.</span></span> <span data-ttu-id="4942b-121">您的 hello 伺服器包含 hello 資料庫 toobe 複寫 hello master 資料庫上執行此陳述式。</span><span class="sxs-lookup"><span data-stu-id="4942b-121">You execute this statement on hello master database of hello server containing hello database toobe replicated.</span></span> <span data-ttu-id="4942b-122">hello 進行地理複寫資料庫 (hello 「 主要資料庫 」) 將會擁有相同的名稱，因為正在進行複寫的 hello 資料庫並將預設 hello hello 相同服務層級為 hello 主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-122">hello geo-replicated database (hello "primary database") will have hello same name as hello database being replicated and will, by default, have hello same service level as hello primary database.</span></span> <span data-ttu-id="4942b-123">hello 次要資料庫可以是可讀取或無法讀取，而且可以是單一資料庫或彈性集區中。</span><span class="sxs-lookup"><span data-stu-id="4942b-123">hello secondary database can be readable or non-readable, and can be a single database or in an elastic pool.</span></span> <span data-ttu-id="4942b-124">如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="4942b-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="4942b-125">建立並植入 hello 次要資料庫之後，資料將會開始從主要資料庫的 hello 以非同步方式複寫。</span><span class="sxs-lookup"><span data-stu-id="4942b-125">After hello secondary database is created and seeded, data will begin replicating asynchronously from hello primary database.</span></span> <span data-ttu-id="4942b-126">hello 下列步驟說明如何 tooconfigure 地理複寫使用 Management Studio。</span><span class="sxs-lookup"><span data-stu-id="4942b-126">hello steps below describe how tooconfigure geo-replication using Management Studio.</span></span> <span data-ttu-id="4942b-127">步驟 toocreate 非可讀取和可讀取次要資料庫，被提供做為單一資料庫或彈性集區中。</span><span class="sxs-lookup"><span data-stu-id="4942b-127">Steps toocreate non-readable and readable secondaries, either as a single database or in an elastic pool, are provided.</span></span>

> [!NOTE]
> <span data-ttu-id="4942b-128">如果以相同的名稱，作為主要的 hello hello hello 指定的夥伴伺服器上的資料庫存在資料庫 hello 命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="4942b-128">If a database exists on hello specified partner server with hello same name as hello primary database hello command will fail.</span></span>
> 

### <a name="add-readable-secondary-single-database"></a><span data-ttu-id="4942b-129">加入可讀取次要複本 (單一資料庫)</span><span class="sxs-lookup"><span data-stu-id="4942b-129">Add readable secondary (single database)</span></span>
<span data-ttu-id="4942b-130">使用下列步驟 toocreate 可讀取的次要複本做為單一資料庫的 hello。</span><span class="sxs-lookup"><span data-stu-id="4942b-130">Use hello following steps toocreate a readable secondary as a single database.</span></span>

1. <span data-ttu-id="4942b-131">在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="4942b-131">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="4942b-132">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4942b-132">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="4942b-133">使用下列 hello **ALTER DATABASE**陳述式 toomake 次要伺服器上的可讀取次要資料庫與異地備援主要的本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-133">Use hello following **ALTER DATABASE** statement toomake a local database into a geo-replication primary with a readable secondary database on a secondary server.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. <span data-ttu-id="4942b-134">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4942b-134">Click **Execute** toorun hello query.</span></span>

### <a name="add-readable-secondary-elastic-pool"></a><span data-ttu-id="4942b-135">新增可讀取次要複本 (彈性集區)</span><span class="sxs-lookup"><span data-stu-id="4942b-135">Add readable secondary (elastic pool)</span></span>
<span data-ttu-id="4942b-136">使用下列步驟 toocreate 彈性集區中的可讀取次要複本的 hello。</span><span class="sxs-lookup"><span data-stu-id="4942b-136">Use hello following steps toocreate a readable secondary in an elastic pool.</span></span>

1. <span data-ttu-id="4942b-137">在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="4942b-137">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="4942b-138">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4942b-138">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="4942b-139">使用下列 hello **ALTER DATABASE**陳述式 toomake 彈性集區中的次要伺服器上的可讀取次要資料庫與異地備援主要的本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-139">Use hello following **ALTER DATABASE** statement toomake a local database into a geo-replication primary with a readable secondary database on a secondary server in an elastic pool.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. <span data-ttu-id="4942b-140">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4942b-140">Click **Execute** toorun hello query.</span></span>

## <a name="remove-secondary-database"></a><span data-ttu-id="4942b-141">移除次要資料庫</span><span class="sxs-lookup"><span data-stu-id="4942b-141">Remove secondary database</span></span>
<span data-ttu-id="4942b-142">您可以使用 hello **ALTER DATABASE**陳述式 toopermanently 終止 hello 與其主要與次要資料庫的複寫合作關係。</span><span class="sxs-lookup"><span data-stu-id="4942b-142">You can use hello **ALTER DATABASE** statement toopermanently terminate hello replication partnership between a secondary database and its primary.</span></span> <span data-ttu-id="4942b-143">主要資料庫所在的 hello hello master 資料庫上執行此陳述式。</span><span class="sxs-lookup"><span data-stu-id="4942b-143">This statement is executed on hello master database on which hello primary database resides.</span></span> <span data-ttu-id="4942b-144">Hello 關聯性終止之後，hello 次要資料庫會變成一般的讀寫資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-144">After hello relationship termination, hello secondary database becomes a regular read-write database.</span></span> <span data-ttu-id="4942b-145">如果 hello 連線 toosecondary 資料庫已損毀 hello 命令會成功，但次要 hello 連線恢復後，將會變成讀寫。</span><span class="sxs-lookup"><span data-stu-id="4942b-145">If hello connectivity toosecondary database is broken hello command succeeds but hello secondary will become read-write after connectivity is restored.</span></span> <span data-ttu-id="4942b-146">如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="4942b-146">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="4942b-147">使用地理複寫合作關係中的下列步驟 tooremove 異地備援的次要的 hello。</span><span class="sxs-lookup"><span data-stu-id="4942b-147">Use hello following steps tooremove geo-replicated secondary from a geo-replication partnership.</span></span>

1. <span data-ttu-id="4942b-148">在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="4942b-148">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="4942b-149">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4942b-149">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="4942b-150">使用下列 hello **ALTER DATABASE**陳述式 tooremove 異地備援的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-150">Use hello following **ALTER DATABASE** statement tooremove a geo-replicated secondary.</span></span>
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. <span data-ttu-id="4942b-151">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4942b-151">Click **Execute** toorun hello query.</span></span>

## <a name="monitor-active-geo-replication-configuration-and-health"></a><span data-ttu-id="4942b-152">監視主動式異地複寫組態和健康狀態</span><span class="sxs-lookup"><span data-stu-id="4942b-152">Monitor active geo-replication configuration and health</span></span>

<span data-ttu-id="4942b-153">監視工作包括 hello 地理複寫組態的監視和監視資料複寫健全狀況。</span><span class="sxs-lookup"><span data-stu-id="4942b-153">Monitoring tasks include monitoring of hello geo-replication configuration and monitoring data replication health.</span></span>  <span data-ttu-id="4942b-154">您可以使用 hello **sys.dm_geo_replication_links** hello master 資料庫 tooreturn 資訊中的每個資料庫的所有現有複寫連結的相關 hello Azure SQL Database 邏輯伺服器上的動態管理檢視。</span><span class="sxs-lookup"><span data-stu-id="4942b-154">You can use hello **sys.dm_geo_replication_links** dynamic management view in hello master database tooreturn information about all exiting replication links for each database on hello Azure SQL Database logical server.</span></span> <span data-ttu-id="4942b-155">此檢視會包含一個資料列，每個主要與次要資料庫之間的 hello 複寫連結。</span><span class="sxs-lookup"><span data-stu-id="4942b-155">This view contains a row for each of hello replication link between primary and secondary databases.</span></span> <span data-ttu-id="4942b-156">您可以使用 hello **sys.dm_replication_link_status**動態管理檢視 tooreturn 一個資料列的每個目前參與複寫的複寫連結的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="4942b-156">You can use hello **sys.dm_replication_link_status** dynamic management view tooreturn a row for each Azure SQL Database that is currently engaged in a replication replication link.</span></span> <span data-ttu-id="4942b-157">這包括主要和次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="4942b-157">This includes both primary and secondary databases.</span></span> <span data-ttu-id="4942b-158">如果在給定主要資料庫有一個以上的連續複寫連結，此資料表會包含 hello 關聯性的每個資料列。</span><span class="sxs-lookup"><span data-stu-id="4942b-158">If more than one continuous replication link exists for a given primary database, this table contains a row for each of hello relationships.</span></span> <span data-ttu-id="4942b-159">在所有資料庫，包括 hello 邏輯 master 中建立 hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="4942b-159">hello view is created in all databases, including hello logical master.</span></span> <span data-ttu-id="4942b-160">不過，查詢在 hello 邏輯 master 中的這個檢視會傳回空集合。</span><span class="sxs-lookup"><span data-stu-id="4942b-160">However, querying this view in hello logical master returns an empty set.</span></span> <span data-ttu-id="4942b-161">您可以使用 hello **sys.dm_operation_status**動態管理檢視 tooshow hello 狀態，進行所有資料庫作業包括 hello hello 複寫連結狀態。</span><span class="sxs-lookup"><span data-stu-id="4942b-161">You can use hello **sys.dm_operation_status** dynamic management view tooshow hello status for all database operations including hello status of hello replication links.</span></span> <span data-ttu-id="4942b-162">如需詳細資訊，請參閱 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx)、[sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 和 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4942b-162">For more information, see [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), and [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).</span></span>

<span data-ttu-id="4942b-163">使用下列步驟 toomonitor 作用中地理複寫合作關係的 hello。</span><span class="sxs-lookup"><span data-stu-id="4942b-163">Use hello following steps toomonitor an active geo-replication partnership.</span></span>

1. <span data-ttu-id="4942b-164">在 Management Studio 中連接 tooyour Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="4942b-164">In Management Studio, connect tooyour Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="4942b-165">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**主要**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4942b-165">Open hello Databases folder, expand hello **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="4942b-166">使用下列陳述式 tooshow hello 所有資料庫的異地複寫連結。</span><span class="sxs-lookup"><span data-stu-id="4942b-166">Use hello following statement tooshow all databases with geo-replication links.</span></span>
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. <span data-ttu-id="4942b-167">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4942b-167">Click **Execute** toorun hello query.</span></span>
5. <span data-ttu-id="4942b-168">開啟 hello 資料庫 資料夾中，展開 hello**系統資料庫**資料夾中，以滑鼠右鍵按一下**MyDB**，然後按一下**新查詢**。</span><span class="sxs-lookup"><span data-stu-id="4942b-168">Open hello Databases folder, expand hello **System Databases** folder, right-click on **MyDB**, and then click **New Query**.</span></span>
6. <span data-ttu-id="4942b-169">下列陳述式 tooshow hello 複寫使用 hello 會延遲，和最後一個 MyDB 我次要資料庫的複寫的時間。</span><span class="sxs-lookup"><span data-stu-id="4942b-169">Use hello following statement tooshow hello replication lags and last replication time of my secondary databases of MyDB.</span></span>
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. <span data-ttu-id="4942b-170">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4942b-170">Click **Execute** toorun hello query.</span></span>
8. <span data-ttu-id="4942b-171">使用下列陳述式 tooshow hello 最新地理複寫作業 MyDB 資料庫相關聯的 hello。</span><span class="sxs-lookup"><span data-stu-id="4942b-171">Use hello following statement tooshow hello most recent geo-replication operations associated with database MyDB.</span></span>
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. <span data-ttu-id="4942b-172">按一下**Execute** toorun hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4942b-172">Click **Execute** toorun hello query.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4942b-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4942b-173">Next steps</span></span>
* <span data-ttu-id="4942b-174">toolearn 深入了解容錯移轉群組和作用中的地理複寫，請參閱-[容錯移轉群組](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4942b-174">toolearn more about failover groups and active geo-replication, see - [Failover groups](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="4942b-175">如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="4942b-175">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>

