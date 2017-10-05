---
title: "轉換現有的資料庫以相應放大 | Microsoft Docs"
description: "建立分區對應管理員來轉換分區化資料庫，以使用彈性資料庫工具"
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
ms.openlocfilehash: 099f40d00753b7c86ba726a818f17d440a125221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="77a07-103">將現有的資料庫移轉到相應放大的資料庫</span><span class="sxs-lookup"><span data-stu-id="77a07-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="77a07-104">使用 Azure SQL Database 資料庫工具 (例如 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md))，輕鬆地管理現有相應放大的分區化資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="77a07-105">您必須先轉換現有的資料庫，才能使用 [分區對應管理員](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="77a07-106">Overview</span><span class="sxs-lookup"><span data-stu-id="77a07-106">Overview</span></span>
<span data-ttu-id="77a07-107">若要移轉現有的分區化資料庫︰</span><span class="sxs-lookup"><span data-stu-id="77a07-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="77a07-108">準備 [分區對應管理員資料庫](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="77a07-109">建立分區對應。</span><span class="sxs-lookup"><span data-stu-id="77a07-109">Create the shard map.</span></span>
3. <span data-ttu-id="77a07-110">準備個別分區。</span><span class="sxs-lookup"><span data-stu-id="77a07-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="77a07-111">將對應新增至分區對應。</span><span class="sxs-lookup"><span data-stu-id="77a07-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="77a07-112">您可以使用 [.NET Framework 用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)或在 [Azure SQL DB - 彈性資料庫工具指令碼](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)中找到的 PowerShell 指令碼，來實作這些技巧。</span><span class="sxs-lookup"><span data-stu-id="77a07-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="77a07-113">以下範例會使用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="77a07-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="77a07-114">如需 ShardMapManager 的詳細資訊，請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="77a07-115">如需彈性資料庫工具的概觀，請參閱 [彈性資料庫功能概觀](sql-database-elastic-scale-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="77a07-116">準備分區對應管理員資料庫</span><span class="sxs-lookup"><span data-stu-id="77a07-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="77a07-117">分區對應管理員是一個特殊的資料庫，其中包含用以管理相應放大之資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="77a07-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="77a07-118">您可以使用現有的資料庫，或建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="77a07-119">請注意，做為分區對應管理員的資料庫不應該是與分區相同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="77a07-120">也請注意，PowerShell 指令碼不會為您建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="77a07-121">步驟 1︰建立分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="77a07-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="77a07-122">擷取分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="77a07-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="77a07-123">在建立之後，您可以使用 Cmdlet 擷取分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="77a07-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="77a07-124">每次需要使用 ShardMapManager 物件，則需要此步驟。</span><span class="sxs-lookup"><span data-stu-id="77a07-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="77a07-125">步驟 2︰建立分區對應</span><span class="sxs-lookup"><span data-stu-id="77a07-125">Step 2: create the shard map</span></span>
<span data-ttu-id="77a07-126">您必須選取要建立的分區對應類型。</span><span class="sxs-lookup"><span data-stu-id="77a07-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="77a07-127">請依據資料庫結構進行選擇︰</span><span class="sxs-lookup"><span data-stu-id="77a07-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="77a07-128">每個資料庫有一個租用戶 (相關詞彙，請參閱 [詞彙](sql-database-elastic-scale-glossary.md))。</span><span class="sxs-lookup"><span data-stu-id="77a07-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="77a07-129">每個資料庫有多個租用戶 (兩種類型)︰</span><span class="sxs-lookup"><span data-stu-id="77a07-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="77a07-130">清單對應</span><span class="sxs-lookup"><span data-stu-id="77a07-130">List mapping</span></span>
   2. <span data-ttu-id="77a07-131">範圍對應</span><span class="sxs-lookup"><span data-stu-id="77a07-131">Range mapping</span></span>

<span data-ttu-id="77a07-132">針對單一租用戶模型，建立 **清單對應** 分區對應。</span><span class="sxs-lookup"><span data-stu-id="77a07-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="77a07-133">單一租用戶模型會指派每個租用戶一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="77a07-134">這是適用於 SaaS 開發人員的有效模式，因為它會簡化管理。</span><span class="sxs-lookup"><span data-stu-id="77a07-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![清單對應][1]

<span data-ttu-id="77a07-136">多租用戶模型會將數個租用戶指派給單一資料庫 (而且您可以跨多個資料庫散發租用戶的群組)。</span><span class="sxs-lookup"><span data-stu-id="77a07-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="77a07-137">預期每個租用戶有小型資料需求時，請使用此模型。</span><span class="sxs-lookup"><span data-stu-id="77a07-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="77a07-138">在此模型中，我們使用 **範圍對應**將某範圍的租用戶指派給資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![範圍對應][2]

<span data-ttu-id="77a07-140">或者，您可以使用「清單對應」  來實作多租用戶資料庫模型，以將多個租用戶指派給單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="77a07-141">例如，DB1 是用來儲存租用戶 ID 1 和 5 的相關資訊，而 DB2 是用來儲存租用戶 7 和租用戶 10 的資料。</span><span class="sxs-lookup"><span data-stu-id="77a07-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![單一資料庫上的多個租用戶][3] 

<span data-ttu-id="77a07-143">**根據您的選擇，選擇下列其中一個選項︰**</span><span class="sxs-lookup"><span data-stu-id="77a07-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="77a07-144">選項 1︰建立清單對應的分區對應</span><span class="sxs-lookup"><span data-stu-id="77a07-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="77a07-145">使用 ShardMapManager 物件建立分區對應。</span><span class="sxs-lookup"><span data-stu-id="77a07-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="77a07-146">選項 2︰建立範圍對應的分區對應</span><span class="sxs-lookup"><span data-stu-id="77a07-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="77a07-147">請注意，若要利用此對應模式，租用戶 ID 值需要是連續的範圍，而且可接受範圍中有間距，方法為只在建立資料庫時略過範圍。</span><span class="sxs-lookup"><span data-stu-id="77a07-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="77a07-148">選項 3︰單一資料庫上的清單對應</span><span class="sxs-lookup"><span data-stu-id="77a07-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="77a07-149">設定此模式也需要建立清單對應，如步驟 2，選項 1 所示。</span><span class="sxs-lookup"><span data-stu-id="77a07-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="77a07-150">步驟 3︰準備個別分區</span><span class="sxs-lookup"><span data-stu-id="77a07-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="77a07-151">將每個分區 (資料庫) 新增至分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="77a07-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="77a07-152">這會準備個別資料庫以儲存對應資訊。</span><span class="sxs-lookup"><span data-stu-id="77a07-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="77a07-153">在每個分區上執行此方法。</span><span class="sxs-lookup"><span data-stu-id="77a07-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="77a07-154">步驟 4︰新增對應</span><span class="sxs-lookup"><span data-stu-id="77a07-154">Step 4: Add mappings</span></span>
<span data-ttu-id="77a07-155">新增對應取決於您所建立的分區對應種類。</span><span class="sxs-lookup"><span data-stu-id="77a07-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="77a07-156">如果已建立清單對應，則會新增清單對應。</span><span class="sxs-lookup"><span data-stu-id="77a07-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="77a07-157">如果已建立範圍對應，則會新增範圍對應。</span><span class="sxs-lookup"><span data-stu-id="77a07-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="77a07-158">選項 1︰對應清單對應的資料</span><span class="sxs-lookup"><span data-stu-id="77a07-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="77a07-159">新增清單對應來對應每個租用戶的資料。</span><span class="sxs-lookup"><span data-stu-id="77a07-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="77a07-160">選項 2︰對應範圍對應的資料</span><span class="sxs-lookup"><span data-stu-id="77a07-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="77a07-161">新增所有租用戶識別碼範圍的範圍對應 - 資料庫關聯︰</span><span class="sxs-lookup"><span data-stu-id="77a07-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="77a07-162">步驟 4 選項 3︰對應單一資料庫上多個租用戶的資料</span><span class="sxs-lookup"><span data-stu-id="77a07-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="77a07-163">對於每個租用戶，執行 Add-ListMapping (上面的選項 1)。</span><span class="sxs-lookup"><span data-stu-id="77a07-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="77a07-164">檢查對應</span><span class="sxs-lookup"><span data-stu-id="77a07-164">Checking the mappings</span></span>
<span data-ttu-id="77a07-165">您可以使用下列命令來查詢現有分區以及與其相關聯之對應的相關資訊 ︰</span><span class="sxs-lookup"><span data-stu-id="77a07-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="77a07-166">摘要</span><span class="sxs-lookup"><span data-stu-id="77a07-166">Summary</span></span>
<span data-ttu-id="77a07-167">一旦完成安裝後，您就可以開始使用彈性資料庫用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="77a07-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="77a07-168">您也可以使用[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)和[多分區查詢](sql-database-elastic-scale-multishard-querying.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="77a07-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77a07-169">Next steps</span></span>
<span data-ttu-id="77a07-170">從 [Azure SQL DB 彈性資料庫工具指令碼](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)取得 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="77a07-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="77a07-171">這些工具也會在 GitHub 上︰ [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools)。</span><span class="sxs-lookup"><span data-stu-id="77a07-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="77a07-172">使用分割合併工具，在多租用戶模型與單一租用戶模型之間來回移動資料。</span><span class="sxs-lookup"><span data-stu-id="77a07-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="77a07-173">請參閱 [分割合併工具](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77a07-174">其他資源</span><span class="sxs-lookup"><span data-stu-id="77a07-174">Additional resources</span></span>
<span data-ttu-id="77a07-175">如需多租用戶型軟體即服務 (SaaS) 資料庫應用程式的常見資料架構模式的資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="77a07-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="77a07-176">問題和功能要求</span><span class="sxs-lookup"><span data-stu-id="77a07-176">Questions and Feature Requests</span></span>
<span data-ttu-id="77a07-177">如有問題，請透過 [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)與我們連絡，如需要求增加功能，請將這些功能新增至 [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="77a07-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

