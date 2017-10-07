---
title: "aaaMigrate 現有資料庫 tooscale 外 |Microsoft 文件"
description: "藉由建立分區對應管理員轉換分區化資料庫 toouse 彈性資料庫工具"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="1f681-103">移轉現有的資料庫 tooscale 外</span><span class="sxs-lookup"><span data-stu-id="1f681-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="1f681-104">輕鬆地管理您現有向外延展分區化資料庫時使用 Azure SQL Database 資料庫工具 (例如 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md))。</span><span class="sxs-lookup"><span data-stu-id="1f681-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="1f681-105">您必須先轉換現有的資料庫 toouse hello 一組[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="1f681-106">概觀</span><span class="sxs-lookup"><span data-stu-id="1f681-106">Overview</span></span>
<span data-ttu-id="1f681-107">toomigrate 現有的分區化資料庫：</span><span class="sxs-lookup"><span data-stu-id="1f681-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="1f681-108">準備 hello[分區對應管理員資料庫](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="1f681-109">建立 hello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-109">Create hello shard map.</span></span>
3. <span data-ttu-id="1f681-110">準備 hello 個別分區。</span><span class="sxs-lookup"><span data-stu-id="1f681-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="1f681-111">新增對應 toohello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="1f681-112">這些技術可以使用任一 hello 實作[.NET Framework 用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)，或 hello PowerShell 指令碼，請參閱[Azure SQL DB 彈性資料庫工具指令碼](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="1f681-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="1f681-113">hello 範例使用 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1f681-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="1f681-114">如需 hello ShardMapManager 的詳細資訊，請參閱[分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="1f681-115">如需 hello 彈性資料庫工具的概觀，請參閱[彈性資料庫功能概觀](sql-database-elastic-scale-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="1f681-116">準備 hello 分區對應管理員資料庫</span><span class="sxs-lookup"><span data-stu-id="1f681-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="1f681-117">hello 分區對應管理員是包含 hello 資料 toomanage 向外延展資料庫的特殊資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f681-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="1f681-118">您可以使用現有的資料庫，或建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f681-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="1f681-119">請注意，資料庫作為分區對應管理員不應 hello 相同資料庫作為分區。</span><span class="sxs-lookup"><span data-stu-id="1f681-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="1f681-120">也請注意 hello PowerShell 指令碼不會為您建立 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f681-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="1f681-121">步驟 1︰建立分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="1f681-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="1f681-122">tooretrieve hello 分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="1f681-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="1f681-123">在建立之後，您可以擷取與這個指令程式的 hello 分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="1f681-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="1f681-124">每次需要 toouse hello ShardMapManager 物件，則需要這個步驟。</span><span class="sxs-lookup"><span data-stu-id="1f681-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="1f681-125">步驟 2： 建立 hello 分區對應</span><span class="sxs-lookup"><span data-stu-id="1f681-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="1f681-126">您必須選取分區對應 toocreate hello 類型。</span><span class="sxs-lookup"><span data-stu-id="1f681-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="1f681-127">hello 選擇取決於 hello 資料庫架構：</span><span class="sxs-lookup"><span data-stu-id="1f681-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="1f681-128">每個資料庫的單一租用戶 (條款，請參閱 hello[詞彙](sql-database-elastic-scale-glossary.md)。)</span><span class="sxs-lookup"><span data-stu-id="1f681-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="1f681-129">每個資料庫的多個租用戶 (兩種類型)︰</span><span class="sxs-lookup"><span data-stu-id="1f681-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="1f681-130">清單對應</span><span class="sxs-lookup"><span data-stu-id="1f681-130">List mapping</span></span>
   2. <span data-ttu-id="1f681-131">範圍對應</span><span class="sxs-lookup"><span data-stu-id="1f681-131">Range mapping</span></span>

<span data-ttu-id="1f681-132">針對單一租用戶模型，建立 **清單對應** 分區對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="1f681-133">hello 單一租用戶模型會指派一個資料庫，每個租用戶。</span><span class="sxs-lookup"><span data-stu-id="1f681-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="1f681-134">這是適用於 SaaS 開發人員的有效模式，因為它會簡化管理。</span><span class="sxs-lookup"><span data-stu-id="1f681-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![清單對應][1]

<span data-ttu-id="1f681-136">hello 多租用戶模型會指派數個租用戶 tooa 單一資料庫 （和分散多個資料庫的租用戶的群組）。</span><span class="sxs-lookup"><span data-stu-id="1f681-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="1f681-137">當您希望產生每個租用戶 toohave 小型資料需要使用此模型。</span><span class="sxs-lookup"><span data-stu-id="1f681-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="1f681-138">在此模型中，我們會將指派租用戶 tooa 資料庫使用的範圍**範圍對應**。</span><span class="sxs-lookup"><span data-stu-id="1f681-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![範圍對應][2]

<span data-ttu-id="1f681-140">您可以實作多租用戶資料庫模型，使用或*清單對應*tooassign 多個租用戶 tooa 單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="1f681-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="1f681-141">例如，DB1 是租用戶識別碼 1 和 5，請使用的 toostore 的資訊，而 DB2 儲存 7 租用戶和租用戶 10 的資料。</span><span class="sxs-lookup"><span data-stu-id="1f681-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![單一資料庫上的多個租用戶][3] 

<span data-ttu-id="1f681-143">**根據您的選擇，選擇下列其中一個選項︰**</span><span class="sxs-lookup"><span data-stu-id="1f681-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="1f681-144">選項 1︰建立清單對應的分區對應</span><span class="sxs-lookup"><span data-stu-id="1f681-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="1f681-145">建立使用 hello ShardMapManager 物件分區對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="1f681-146">選項 2︰建立範圍對應的分區對應</span><span class="sxs-lookup"><span data-stu-id="1f681-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="1f681-147">請注意該 tooutilize 此對應模式、 租用戶的識別碼值需要 toobe 連續範圍，而它是 hello 範圍中的可接受 toohave 間隔藉由建立 hello 資料庫時，只略過 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="1f681-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="1f681-148">選項 3︰單一資料庫上的清單對應</span><span class="sxs-lookup"><span data-stu-id="1f681-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="1f681-149">設定此模式也需要建立清單對應，如步驟 2，選項 1 所示。</span><span class="sxs-lookup"><span data-stu-id="1f681-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="1f681-150">步驟 3︰準備個別分區</span><span class="sxs-lookup"><span data-stu-id="1f681-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="1f681-151">加入每個分區 （資料庫） toohello 分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="1f681-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="1f681-152">這會準備 hello 個別資料庫儲存對應資訊。</span><span class="sxs-lookup"><span data-stu-id="1f681-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="1f681-153">在每個分區上執行此方法。</span><span class="sxs-lookup"><span data-stu-id="1f681-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="1f681-154">步驟 4︰新增對應</span><span class="sxs-lookup"><span data-stu-id="1f681-154">Step 4: Add mappings</span></span>
<span data-ttu-id="1f681-155">對應的 hello 加法取決於您所建立的分區對應 hello 種類。</span><span class="sxs-lookup"><span data-stu-id="1f681-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="1f681-156">如果已建立清單對應，則會新增清單對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="1f681-157">如果已建立範圍對應，則會新增範圍對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="1f681-158">清單對應的選項 1： 對應 hello 資料</span><span class="sxs-lookup"><span data-stu-id="1f681-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="1f681-159">Hello 資料對應每個租用戶加入清單的對應。</span><span class="sxs-lookup"><span data-stu-id="1f681-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="1f681-160">選項 2： 地圖 hello 資料範圍的對應</span><span class="sxs-lookup"><span data-stu-id="1f681-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="1f681-161">加入所有的 hello 租用戶識別碼範圍-資料庫關聯的 hello 範圍對應：</span><span class="sxs-lookup"><span data-stu-id="1f681-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="1f681-162">步驟 4 選項 3: hello 資料對應的單一資料庫上的多個租用戶</span><span class="sxs-lookup"><span data-stu-id="1f681-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="1f681-163">每個租用戶，執行新增 ListMapping hello （選項 1，上方）。</span><span class="sxs-lookup"><span data-stu-id="1f681-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="1f681-164">檢查 hello 對應</span><span class="sxs-lookup"><span data-stu-id="1f681-164">Checking hello mappings</span></span>
<span data-ttu-id="1f681-165">您可以使用下列命令查詢 hello 現有分區和與其相關聯的 hello 對應的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="1f681-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="1f681-166">摘要</span><span class="sxs-lookup"><span data-stu-id="1f681-166">Summary</span></span>
<span data-ttu-id="1f681-167">當您完成 hello 安裝程式時，您可以開始 toouse hello 彈性資料庫用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="1f681-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="1f681-168">您也可以使用[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)和[多分區查詢](sql-database-elastic-scale-multishard-querying.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f681-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f681-169">Next steps</span></span>
<span data-ttu-id="1f681-170">取得從 hello PowerShell 指令碼[Azure SQL DB 彈性資料庫工具 sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="1f681-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="1f681-171">hello 工具也會在 GitHub 上： [Azure/彈性-db-tools](https://github.com/Azure/elastic-db-tools)。</span><span class="sxs-lookup"><span data-stu-id="1f681-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="1f681-172">使用來自多租用戶模型 tooa 單一租用戶模型 hello 分割合併工具 toomove 資料 tooor。</span><span class="sxs-lookup"><span data-stu-id="1f681-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="1f681-173">請參閱 [分割合併工具](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f681-174">其他資源</span><span class="sxs-lookup"><span data-stu-id="1f681-174">Additional resources</span></span>
<span data-ttu-id="1f681-175">如需多租用戶型軟體即服務 (SaaS) 資料庫應用程式的常見資料架構模式的資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="1f681-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="1f681-176">問題和功能要求</span><span class="sxs-lookup"><span data-stu-id="1f681-176">Questions and Feature Requests</span></span>
<span data-ttu-id="1f681-177">如有問題，請聯繫 toous 上 hello [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)和功能的要求，請將它們加入 toohello [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="1f681-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

