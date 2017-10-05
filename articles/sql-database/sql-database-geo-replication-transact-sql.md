---
title: "使用 Transact-SQL 為 Azure SQL Database 設定異地複寫 | Microsoft Docs"
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
ms.openlocfilehash: e5011c1c67e051616d53621b72e46ba894ca3c02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a><span data-ttu-id="f6021-103">使用 Transact-SQL 為 Azure SQL Database 設定作用中異地複寫</span><span class="sxs-lookup"><span data-stu-id="f6021-103">Configure active geo-replication for Azure SQL Database with Transact-SQL</span></span>

<span data-ttu-id="f6021-104">本文說明如何使用 Transact-SQL，為 Azure SQL Database 設定主動式異地複寫。</span><span class="sxs-lookup"><span data-stu-id="f6021-104">This article shows you how to configure active geo-replication for an Azure SQL Database with Transact-SQL.</span></span>

<span data-ttu-id="f6021-105">若要使用 Transact-SQL 起始容錯移轉，請參閱 [使用 Transact-SQL 為 Azure SQL Database 起始計劃性或非計劃性容錯移轉](sql-database-geo-replication-failover-transact-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="f6021-105">To initiate failover using Transact-SQL, see [Initiate a planned or unplanned failover for Azure SQL Database with Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f6021-106">當您使用主動式異地複寫 (可讀取次要複本) 進行災害復原時，您應該為應用程式內的所有資料庫設定容錯移轉群組以啟用自動且通透的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="f6021-106">When you use active geo-replication (readable secondaries) for disaster recovery you should configure a failover group for all databases within an application to enable automatic and transparent failover.</span></span> <span data-ttu-id="f6021-107">這項功能處於預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="f6021-107">This feature is in preview.</span></span> <span data-ttu-id="f6021-108">如需詳細資訊，請參閱[自動容錯移轉群組和異地複寫](sql-database-geo-replication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f6021-108">For more information see [Auto-failover groups and geo-replication](sql-database-geo-replication-overview.md).</span></span>
> 
> 

<span data-ttu-id="f6021-109">若要使用 Transact-SQL 設定主動式異地複寫，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f6021-109">To configure active geo-replication using Transact-SQL, you need the following:</span></span>

* <span data-ttu-id="f6021-110">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f6021-110">An Azure subscription</span></span>
* <span data-ttu-id="f6021-111">邏輯 Azure SQL Database 伺服器 <MyLocalServer> 和 SQL Database <MyDB> - 您想要複寫的主要資料庫</span><span class="sxs-lookup"><span data-stu-id="f6021-111">A logical Azure SQL Database server <MyLocalServer> and a SQL database <MyDB> - The primary database that you want to replicate</span></span>
* <span data-ttu-id="f6021-112">一或多個邏輯 Azure SQL Database 伺服器 <MySecondaryServer(n)> - 您將在其中建立次要資料庫的夥伴伺服器的邏輯伺服器</span><span class="sxs-lookup"><span data-stu-id="f6021-112">One or more logical Azure SQL Database servers <MySecondaryServer(n)> - The logical servers that will be the partner servers in which you will create secondary databases</span></span>
* <span data-ttu-id="f6021-113">主要資料庫上的 DBManager 登入</span><span class="sxs-lookup"><span data-stu-id="f6021-113">A login that is DBManager on the primary</span></span>
* <span data-ttu-id="f6021-114">擁有您要異地複寫之本機資料庫的 db_ownership</span><span class="sxs-lookup"><span data-stu-id="f6021-114">Have db_ownership of the local database that you will geo-replicate</span></span>
* <span data-ttu-id="f6021-115">成為您為異地複寫所設定之夥伴伺服器上的 DBManager</span><span class="sxs-lookup"><span data-stu-id="f6021-115">Be DBManager on the partner server(s) to which you will configure geo-replication</span></span>
* <span data-ttu-id="f6021-116">最新版的 SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="f6021-116">The newest version of SQL Server Management Studio (SSMS)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6021-117">建議您一律使用最新版本的 Management Studio 保持與 Microsoft Azure 及 SQL Database 更新同步。</span><span class="sxs-lookup"><span data-stu-id="f6021-117">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="f6021-118">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6021-118">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

## <a name="add-secondary-database"></a><span data-ttu-id="f6021-119">加入次要資料庫</span><span class="sxs-lookup"><span data-stu-id="f6021-119">Add secondary database</span></span>
<span data-ttu-id="f6021-120">您可以使用 **ALTER DATABASE** 陳述式，在夥伴伺服器上建立異地複寫的次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6021-120">You can use the **ALTER DATABASE** statement to create a geo-replicated secondary database on a partner server.</span></span> <span data-ttu-id="f6021-121">您在包含要複寫的資料庫伺服器的 master 資料庫上執行此陳述式。</span><span class="sxs-lookup"><span data-stu-id="f6021-121">You execute this statement on the master database of the server containing the database to be replicated.</span></span> <span data-ttu-id="f6021-122">異地複寫資料庫 (「主要資料庫」) 會具備與要複寫的資料庫相同的名稱，並且預設與主要資料庫具有相同的服務層級。</span><span class="sxs-lookup"><span data-stu-id="f6021-122">The geo-replicated database (the "primary database") will have the same name as the database being replicated and will, by default, have the same service level as the primary database.</span></span> <span data-ttu-id="f6021-123">次要資料庫可以是可讀取或不可讀取，並且可以是單一資料庫或彈性集區。</span><span class="sxs-lookup"><span data-stu-id="f6021-123">The secondary database can be readable or non-readable, and can be a single database or in an elastic pool.</span></span> <span data-ttu-id="f6021-124">如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="f6021-124">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="f6021-125">建立次要資料庫並植入之後，資料就會開始以非同步方式從主要資料庫複寫。</span><span class="sxs-lookup"><span data-stu-id="f6021-125">After the secondary database is created and seeded, data will begin replicating asynchronously from the primary database.</span></span> <span data-ttu-id="f6021-126">下列步驟說明如何使用 Management Studio 來設定異地複寫。</span><span class="sxs-lookup"><span data-stu-id="f6021-126">The steps below describe how to configure geo-replication using Management Studio.</span></span> <span data-ttu-id="f6021-127">提供使用單一資料庫或彈性集區建立不可讀取和可讀取次要複本的步驟。</span><span class="sxs-lookup"><span data-stu-id="f6021-127">Steps to create non-readable and readable secondaries, either as a single database or in an elastic pool, are provided.</span></span>

> [!NOTE]
> <span data-ttu-id="f6021-128">如果指定的夥伴伺服器上存在與名稱與主要資料庫相同的資料庫，則命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="f6021-128">If a database exists on the specified partner server with the same name as the primary database the command will fail.</span></span>
> 

### <a name="add-readable-secondary-single-database"></a><span data-ttu-id="f6021-129">加入可讀取次要複本 (單一資料庫)</span><span class="sxs-lookup"><span data-stu-id="f6021-129">Add readable secondary (single database)</span></span>
<span data-ttu-id="f6021-130">您可以使用下列步驟，將可讀取次要複本建立為單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6021-130">Use the following steps to create a readable secondary as a single database.</span></span>

1. <span data-ttu-id="f6021-131">在 Management Studio 中，連接到您的 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6021-131">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="f6021-132">開啟 Databases 資料夾、展開 [System Databases] 資料夾、在 [master] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="f6021-132">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="f6021-133">使用下列 **ALTER DATABASE** 陳述式，使本機資料庫成為一個在次要伺服器上具有可讀取之次要資料庫的異地複寫主要複本。</span><span class="sxs-lookup"><span data-stu-id="f6021-133">Use the following **ALTER DATABASE** statement to make a local database into a geo-replication primary with a readable secondary database on a secondary server.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. <span data-ttu-id="f6021-134">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f6021-134">Click **Execute** to run the query.</span></span>

### <a name="add-readable-secondary-elastic-pool"></a><span data-ttu-id="f6021-135">新增可讀取次要複本 (彈性集區)</span><span class="sxs-lookup"><span data-stu-id="f6021-135">Add readable secondary (elastic pool)</span></span>
<span data-ttu-id="f6021-136">您可以使用下列步驟，在彈性集區中建立可讀取次要複本。</span><span class="sxs-lookup"><span data-stu-id="f6021-136">Use the following steps to create a readable secondary in an elastic pool.</span></span>

1. <span data-ttu-id="f6021-137">在 Management Studio 中，連接到您的 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6021-137">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="f6021-138">開啟 Databases 資料夾、展開 [System Databases] 資料夾、在 [master] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="f6021-138">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="f6021-139">使用下列 **ALTER DATABASE** 陳述式，使本機資料庫成為一個在彈性集區中次要伺服器上具有可讀取之次要資料庫的異地複寫主要複本。</span><span class="sxs-lookup"><span data-stu-id="f6021-139">Use the following **ALTER DATABASE** statement to make a local database into a geo-replication primary with a readable secondary database on a secondary server in an elastic pool.</span></span>
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. <span data-ttu-id="f6021-140">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f6021-140">Click **Execute** to run the query.</span></span>

## <a name="remove-secondary-database"></a><span data-ttu-id="f6021-141">移除次要資料庫</span><span class="sxs-lookup"><span data-stu-id="f6021-141">Remove secondary database</span></span>
<span data-ttu-id="f6021-142">您可以使用 **ALTER DATABASE** 陳述式以永久終止次要資料庫與其主要資料庫之間的複寫關係。</span><span class="sxs-lookup"><span data-stu-id="f6021-142">You can use the **ALTER DATABASE** statement to permanently terminate the replication partnership between a secondary database and its primary.</span></span> <span data-ttu-id="f6021-143">此陳述式是在主要資料庫所在的 master 資料庫上執行。</span><span class="sxs-lookup"><span data-stu-id="f6021-143">This statement is executed on the master database on which the primary database resides.</span></span> <span data-ttu-id="f6021-144">關聯性終止之後，次要資料庫會成為一般的讀寫資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6021-144">After the relationship termination, the secondary database becomes a regular read-write database.</span></span> <span data-ttu-id="f6021-145">如果與次要資料庫的連線中斷，命令將會成功，但次要資料庫必須等到連線恢復後才會變成可讀寫。</span><span class="sxs-lookup"><span data-stu-id="f6021-145">If the connectivity to secondary database is broken the command succeeds but the secondary will become read-write after connectivity is restored.</span></span> <span data-ttu-id="f6021-146">如需詳細資訊，請參閱 [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) 和[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="f6021-146">For more information, see [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) and [Service Tiers](sql-database-service-tiers.md).</span></span>

<span data-ttu-id="f6021-147">使用下列步驟可從異地複寫合作關係中移除異地複寫的次要複本。</span><span class="sxs-lookup"><span data-stu-id="f6021-147">Use the following steps to remove geo-replicated secondary from a geo-replication partnership.</span></span>

1. <span data-ttu-id="f6021-148">在 Management Studio 中，連接到您的 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6021-148">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="f6021-149">開啟 Databases 資料夾、展開 [System Databases] 資料夾、在 [master] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="f6021-149">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="f6021-150">使用下列 **ALTER DATABASE** 陳述式來移除異地複寫的次要複本。</span><span class="sxs-lookup"><span data-stu-id="f6021-150">Use the following **ALTER DATABASE** statement to remove a geo-replicated secondary.</span></span>
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. <span data-ttu-id="f6021-151">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f6021-151">Click **Execute** to run the query.</span></span>

## <a name="monitor-active-geo-replication-configuration-and-health"></a><span data-ttu-id="f6021-152">監視主動式異地複寫組態和健康狀態</span><span class="sxs-lookup"><span data-stu-id="f6021-152">Monitor active geo-replication configuration and health</span></span>

<span data-ttu-id="f6021-153">監視工作包括異地複寫組態的監視和監視資料複寫健康狀態。</span><span class="sxs-lookup"><span data-stu-id="f6021-153">Monitoring tasks include monitoring of the geo-replication configuration and monitoring data replication health.</span></span>  <span data-ttu-id="f6021-154">您可以使用 master 資料庫中的 **sys.dm_geo_replication_links** 動態管理檢視，傳回 Azure SQL Database 邏輯伺服器上每個資料庫的所有現有複寫連結的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f6021-154">You can use the **sys.dm_geo_replication_links** dynamic management view in the master database to return information about all exiting replication links for each database on the Azure SQL Database logical server.</span></span> <span data-ttu-id="f6021-155">這個檢視針對每個主要和次要資料庫之間的複寫連結包含一個資料列。</span><span class="sxs-lookup"><span data-stu-id="f6021-155">This view contains a row for each of the replication link between primary and secondary databases.</span></span> <span data-ttu-id="f6021-156">您可以使用 **sys.dm_replication_link_status** 動態管理檢視，對目前參與複寫連結的每個 Azure SQL Database 傳回一個資料列。</span><span class="sxs-lookup"><span data-stu-id="f6021-156">You can use the **sys.dm_replication_link_status** dynamic management view to return a row for each Azure SQL Database that is currently engaged in a replication replication link.</span></span> <span data-ttu-id="f6021-157">這包括主要和次要資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6021-157">This includes both primary and secondary databases.</span></span> <span data-ttu-id="f6021-158">如果給定主要資料庫有一個以上的連續複寫連結，此資料表會對每個關聯性包含一個資料列。</span><span class="sxs-lookup"><span data-stu-id="f6021-158">If more than one continuous replication link exists for a given primary database, this table contains a row for each of the relationships.</span></span> <span data-ttu-id="f6021-159">會在所有資料庫 (包括邏輯主機) 中建立檢視。</span><span class="sxs-lookup"><span data-stu-id="f6021-159">The view is created in all databases, including the logical master.</span></span> <span data-ttu-id="f6021-160">不過，在邏輯主機中查詢此檢視會傳回空集合。</span><span class="sxs-lookup"><span data-stu-id="f6021-160">However, querying this view in the logical master returns an empty set.</span></span> <span data-ttu-id="f6021-161">您可以使用 **sys.dm_operation_status** 動態管理檢視來顯示所有資料庫作業的狀態，包括複寫連結的狀態。</span><span class="sxs-lookup"><span data-stu-id="f6021-161">You can use the **sys.dm_operation_status** dynamic management view to show the status for all database operations including the status of the replication links.</span></span> <span data-ttu-id="f6021-162">如需詳細資訊，請參閱 [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx)、[sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx) 和 [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6021-162">For more information, see [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), and [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).</span></span>

<span data-ttu-id="f6021-163">使用下列步驟可監視作用中異地複寫合作關係。</span><span class="sxs-lookup"><span data-stu-id="f6021-163">Use the following steps to monitor an active geo-replication partnership.</span></span>

1. <span data-ttu-id="f6021-164">在 Management Studio 中，連接到您的 Azure SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6021-164">In Management Studio, connect to your Azure SQL Database logical server.</span></span>
2. <span data-ttu-id="f6021-165">開啟 Databases 資料夾、展開 [System Databases] 資料夾、在 [master] 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="f6021-165">Open the Databases folder, expand the **System Databases** folder, right-click on **master**, and then click **New Query**.</span></span>
3. <span data-ttu-id="f6021-166">使用下列陳述式可顯示具有異地複寫連結的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="f6021-166">Use the following statement to show all databases with geo-replication links.</span></span>
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. <span data-ttu-id="f6021-167">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f6021-167">Click **Execute** to run the query.</span></span>
5. <span data-ttu-id="f6021-168">開啟 Databases 資料夾、展開 **System Databases** 資料夾、在 **MyDB** 上按一下滑鼠右鍵，然後按一下 [新增查詢]。</span><span class="sxs-lookup"><span data-stu-id="f6021-168">Open the Databases folder, expand the **System Databases** folder, right-click on **MyDB**, and then click **New Query**.</span></span>
6. <span data-ttu-id="f6021-169">使用下列陳述式來顯示複寫落後和我的次要資料庫 MyDB 上次複寫的開始時間。</span><span class="sxs-lookup"><span data-stu-id="f6021-169">Use the following statement to show the replication lags and last replication time of my secondary databases of MyDB.</span></span>
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. <span data-ttu-id="f6021-170">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f6021-170">Click **Execute** to run the query.</span></span>
8. <span data-ttu-id="f6021-171">使用下列陳述式可顯示與 MyDB 資料庫相關聯的最新異地複寫作業。</span><span class="sxs-lookup"><span data-stu-id="f6021-171">Use the following statement to show the most recent geo-replication operations associated with database MyDB.</span></span>
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. <span data-ttu-id="f6021-172">按一下 [執行]  來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f6021-172">Click **Execute** to run the query.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6021-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6021-173">Next steps</span></span>
* <span data-ttu-id="f6021-174">若要深入了解容錯移轉群組與主動式異地複寫的詳細資訊，請參閱[容錯移轉群組](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f6021-174">To learn more about failover groups and active geo-replication, see - [Failover groups](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="f6021-175">如需商務持續性概觀和案例，請參閱 [商務持續性概觀](sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="f6021-175">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md)</span></span>

