---
title: "相應放大 Azure SQL Database | Microsoft Docs"
description: "如何使用彈性資料庫用戶端程式庫 ShardMapManager"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f626cf417d8b3f1761f3c900d49039b3ff83b093
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="fa4b1-103">使用分區對應管理員相應放大資料庫</span><span class="sxs-lookup"><span data-stu-id="fa4b1-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="fa4b1-104">若要在 SQL Azure 上輕鬆地相應放大資料庫，請使用分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="fa4b1-105">分區對應管理員是特殊的資料庫，負責維護分區集中所有分區 (資料庫) 的全域對應資訊。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="fa4b1-106">此中繼資料可讓應用程式根據 **分區化索引鍵**的值，連線到正確的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="fa4b1-107">此外，分區集中的每個分區都包含可追蹤本機分區資料的對應 (稱為 **shardlet**)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![分區對應管理](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="fa4b1-109">了解這些對應建構的方式，是分區對應管理的基本。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="fa4b1-110">使用可在[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)中找到的 [ShardMapManager 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)來管理分區對應，即可達成。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="fa4b1-111">分區對應和分區對應方式</span><span class="sxs-lookup"><span data-stu-id="fa4b1-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="fa4b1-112">對於每個分區，您必須選取要建立的分區對應類型。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="fa4b1-113">請依據資料庫結構進行選擇︰</span><span class="sxs-lookup"><span data-stu-id="fa4b1-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="fa4b1-114">每個資料庫的單一租用戶</span><span class="sxs-lookup"><span data-stu-id="fa4b1-114">Single tenant per database</span></span>  
2. <span data-ttu-id="fa4b1-115">每個資料庫的多個租用戶 (兩種類型)︰</span><span class="sxs-lookup"><span data-stu-id="fa4b1-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="fa4b1-116">清單對應</span><span class="sxs-lookup"><span data-stu-id="fa4b1-116">List mapping</span></span>
   2. <span data-ttu-id="fa4b1-117">範圍對應</span><span class="sxs-lookup"><span data-stu-id="fa4b1-117">Range mapping</span></span>

<span data-ttu-id="fa4b1-118">針對單一租用戶模型，建立 **清單對應** 分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="fa4b1-119">單一租用戶模型會指派每個租用戶一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="fa4b1-120">這是適用於 SaaS 開發人員的有效模式，因為它會簡化管理。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![清單對應][1]

<span data-ttu-id="fa4b1-122">多租用戶模型會將數個租用戶指派給單一資料庫 (而且您可以跨多個資料庫散發租用戶的群組)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="fa4b1-123">預期每個租用戶有小型資料需求時，請使用此模型。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="fa4b1-124">在此模型中，我們使用 **範圍對應**將某範圍的租用戶指派給資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![範圍對應][2]

<span data-ttu-id="fa4b1-126">或者，您可以使用「清單對應」  來實作多租用戶資料庫模型，以將多個租用戶指派給單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="fa4b1-127">例如，DB1 是用來儲存租用戶 ID 1 和 5 的相關資訊，而 DB2 是用來儲存租用戶 7 和租用戶 10 的資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![單一資料庫上的多個租用戶][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="fa4b1-129">分區化索引鍵支援的 .Net 型別</span><span class="sxs-lookup"><span data-stu-id="fa4b1-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="fa4b1-130">Elastic Scale 支援下列 .Net Framework 型別作為分區化索引鍵：</span><span class="sxs-lookup"><span data-stu-id="fa4b1-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="fa4b1-131">integer</span><span class="sxs-lookup"><span data-stu-id="fa4b1-131">integer</span></span>
* <span data-ttu-id="fa4b1-132">long</span><span class="sxs-lookup"><span data-stu-id="fa4b1-132">long</span></span>
* <span data-ttu-id="fa4b1-133">guid</span><span class="sxs-lookup"><span data-stu-id="fa4b1-133">guid</span></span>
* <span data-ttu-id="fa4b1-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="fa4b1-134">byte[]</span></span>  
* <span data-ttu-id="fa4b1-135">datetime</span><span class="sxs-lookup"><span data-stu-id="fa4b1-135">datetime</span></span>
* <span data-ttu-id="fa4b1-136">timespan</span><span class="sxs-lookup"><span data-stu-id="fa4b1-136">timespan</span></span>
* <span data-ttu-id="fa4b1-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fa4b1-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="fa4b1-138">清單和範圍分區對應</span><span class="sxs-lookup"><span data-stu-id="fa4b1-138">List and range shard maps</span></span>
<span data-ttu-id="fa4b1-139">建構分區對應時可以選擇使用**個別分區化索引鍵值的清單**，或使用**分區化索引鍵值的範圍**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="fa4b1-140">清單分區對應</span><span class="sxs-lookup"><span data-stu-id="fa4b1-140">List shard maps</span></span>
<span data-ttu-id="fa4b1-141">**分區**包含 **Shardlet**，Shardlet 至分區的對應是由分區對應所維護。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="fa4b1-142">**清單分區對應** 是個別索引鍵值 (識別 Shardlet) 與資料庫 (做為分區) 之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="fa4b1-143">**清單對應** 十分明確，而且不同的索引鍵值可以對應到相同資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="fa4b1-144">例如，索引鍵 1 對應到 Database A，索引鍵值 3 和 6 都參照 Database B。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="fa4b1-145">金鑰</span><span class="sxs-lookup"><span data-stu-id="fa4b1-145">Key</span></span> | <span data-ttu-id="fa4b1-146">分區位置</span><span class="sxs-lookup"><span data-stu-id="fa4b1-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="fa4b1-147">1</span><span class="sxs-lookup"><span data-stu-id="fa4b1-147">1</span></span> |<span data-ttu-id="fa4b1-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="fa4b1-148">Database_A</span></span> |
| <span data-ttu-id="fa4b1-149">3</span><span class="sxs-lookup"><span data-stu-id="fa4b1-149">3</span></span> |<span data-ttu-id="fa4b1-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="fa4b1-150">Database_B</span></span> |
| <span data-ttu-id="fa4b1-151">4</span><span class="sxs-lookup"><span data-stu-id="fa4b1-151">4</span></span> |<span data-ttu-id="fa4b1-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="fa4b1-152">Database_C</span></span> |
| <span data-ttu-id="fa4b1-153">6</span><span class="sxs-lookup"><span data-stu-id="fa4b1-153">6</span></span> |<span data-ttu-id="fa4b1-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="fa4b1-154">Database_B</span></span> |
| <span data-ttu-id="fa4b1-155">...</span><span class="sxs-lookup"><span data-stu-id="fa4b1-155">...</span></span> |<span data-ttu-id="fa4b1-156">...</span><span class="sxs-lookup"><span data-stu-id="fa4b1-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="fa4b1-157">範圍分區對應</span><span class="sxs-lookup"><span data-stu-id="fa4b1-157">Range shard maps</span></span>
<span data-ttu-id="fa4b1-158">在**範圍分區對應**中，由一組 **[低值, 高值)** 描述索引鍵範圍，其中*低值*是範圍內的最小索引鍵，*高值*是高於該範圍的第一個值。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="fa4b1-159">例如，**[0, 100)** 包含所有大於或等於 0 且小於 100 的整數。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="fa4b1-160">請注意，多個範圍可指向相同的資料庫，而且可支援不相連的範圍 (例如 [100, 200) 和 [400, 600) 都指向下面範例中的資料庫 C。)</span><span class="sxs-lookup"><span data-stu-id="fa4b1-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="fa4b1-161">金鑰</span><span class="sxs-lookup"><span data-stu-id="fa4b1-161">Key</span></span> | <span data-ttu-id="fa4b1-162">分區位置</span><span class="sxs-lookup"><span data-stu-id="fa4b1-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="fa4b1-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="fa4b1-163">[1,50)</span></span> |<span data-ttu-id="fa4b1-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="fa4b1-164">Database_A</span></span> |
| <span data-ttu-id="fa4b1-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="fa4b1-165">[50,100)</span></span> |<span data-ttu-id="fa4b1-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="fa4b1-166">Database_B</span></span> |
| <span data-ttu-id="fa4b1-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="fa4b1-167">[100,200)</span></span> |<span data-ttu-id="fa4b1-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="fa4b1-168">Database_C</span></span> |
| <span data-ttu-id="fa4b1-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="fa4b1-169">[400,600)</span></span> |<span data-ttu-id="fa4b1-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="fa4b1-170">Database_C</span></span> |
| <span data-ttu-id="fa4b1-171">...</span><span class="sxs-lookup"><span data-stu-id="fa4b1-171">...</span></span> |<span data-ttu-id="fa4b1-172">...</span><span class="sxs-lookup"><span data-stu-id="fa4b1-172">...</span></span> |

<span data-ttu-id="fa4b1-173">上述每個資料表都是 **ShardMap** 物件的概念範例。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="fa4b1-174">每個資料列是個別 **PointMapping** (適用於清單分區對應) 或 **RangeMapping** (適用於範圍分區對應) 物件的簡化範例。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="fa4b1-175">分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="fa4b1-175">Shard map manager</span></span>
<span data-ttu-id="fa4b1-176">在用戶端程式庫中，分區對應管理員是分區對應的集合。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="fa4b1-177">**ShardMapManager** 執行個體所管理的資料會保留在三個位置：</span><span class="sxs-lookup"><span data-stu-id="fa4b1-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="fa4b1-178">**全域分區對應 (GSM)**：您指定資料庫作為其所有分區對應及對應的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="fa4b1-179">自動會建立特殊的資料表和預存程序來管理資訊。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="fa4b1-180">這通常是一個小型資料庫且很少存取，且不應該用於應用程式的其他需求。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="fa4b1-181">資料表位於一個名為 **__ShardManagement** 的特殊結構描述中。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="fa4b1-182">**本機分區對應 (LSM)**：您指定作為分區的每個資料庫會修改成包含數個小型資料表和特殊預存程序，其中包含並管理該分區特有的分區對應資訊。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="fa4b1-183">這項資訊與 GSM 中的資訊重複，並可讓應用程式驗證快取的分區對應資訊，而不會對 GSM 造成任何負擔；應用程式使用 LSM 判斷快取的對應是否仍然有效。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="fa4b1-184">每個分區上對應至 LSM 的每個資料表，也會在結構描述 **__ShardManagement** 中。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="fa4b1-185">**應用程式快取**：每個存取 **ShardMapManager** 物件的應用程式執行個體會維護其對應的本機記憶體內部快取。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="fa4b1-186">它會儲存最近擷取的路由資訊。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="fa4b1-187">建構 ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="fa4b1-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="fa4b1-188">**ShardMapManager** 物件是使用 [Factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) 模式所建構。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="fa4b1-189">**[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** 方法接受 **ConnectionString** 形式的認證 (包含保留 GSM 的伺服器名稱和資料庫名稱)，並傳回 **ShardMapManager** 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="fa4b1-190">**請注意：**對於每個應用程式網域，**ShardMapManager** 應該只具現化一次 (在應用程式的初始化程式碼內)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="fa4b1-191">如果在相同的應用程式網域中建立 ShardMapManager 的其他執行個體，將會導致應用程式的記憶體和 CPU 使用率增加。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="fa4b1-192">**ShardMapManager** 可以包含任意數目的分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="fa4b1-193">雖然單一分區對應可能足夠用於許多應用程式，但有時幾組不同的資料庫會用於不同的結構描述或做為特殊用途；在這些情況下，最好使用多個分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="fa4b1-194">在這段程式碼中，應用程式會以 **TryGetSqlShardMapManager 方法** 嘗試開啟現有的 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="fa4b1-195">如果代表全域 **ShardMapManager** (GSM) 的物件尚不存在資料庫內，用戶端程式庫會使用 [CreateSqlShardMapManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)在其中建立這些物件。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="fa4b1-196">或者，您也可以使用 Powershell 建立新的分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="fa4b1-197">範例請見 [這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="fa4b1-198">取得 RangeShardMap 或 ListShardMap</span><span class="sxs-lookup"><span data-stu-id="fa4b1-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="fa4b1-199">建立分區對應管理員之後，您可以使用 [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)[TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) 或 [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 方法來取得 [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) 或 [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="fa4b1-200">分區對應系統管理認證</span><span class="sxs-lookup"><span data-stu-id="fa4b1-200">Shard map administration credentials</span></span>
<span data-ttu-id="fa4b1-201">負責管理和操作分區對應的應用程式，不同於使用分區對應來安排連線的分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="fa4b1-202">若要管理分區對應 (加入或變更分區、分區對應 (shard map)、分區對應 (shard mapping) 等等)，您必須使用**在 GSM 資料庫和每一個作為分區的資料庫上擁有讀取/寫入權限的認證**，以具現化 **ShardMapManager**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="fa4b1-203">這些認證必須允許在輸入或變更分區對應資訊時，能夠在 GSM 和 LSM 中寫入資料表，也必須允許在新的分區上建立 LSM 資料表。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="fa4b1-204">請參閱 [用來存取彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="fa4b1-205">只影響中繼資料</span><span class="sxs-lookup"><span data-stu-id="fa4b1-205">Only metadata affected</span></span>
<span data-ttu-id="fa4b1-206">用來填入或變更 **ShardMapManager** 資料的方法不會改變分區本身中儲存的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="fa4b1-207">比方說，**CreateShard**、**DeleteShard**、**UpdateMapping** 等方法只會影響分區對應中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="fa4b1-208">它們不會移除、新增或改變分區中所包含的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="fa4b1-209">相反地，這些方法是設計來搭配其他作業一起使用，例如，您可能執行這些作業來建立或移除實際的資料庫，或將資料列從一個分區移至另一個分區，以重新平衡分區化環境。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="fa4b1-210">(彈性資料庫工具隨附的**分割合併**工具會使用這些 API，以及協調分區之間實際的資料移動。)請參閱[使用彈性資料庫分割合併工具來縮放](sql-database-elastic-scale-overview-split-and-merge.md)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="fa4b1-211">填入分區對應範例</span><span class="sxs-lookup"><span data-stu-id="fa4b1-211">Populating a shard map example</span></span>
<span data-ttu-id="fa4b1-212">填入特定分區對應的作業順序範例如下所示。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="fa4b1-213">程式碼會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa4b1-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="fa4b1-214">在分區對應管理員內建立新的分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="fa4b1-215">將兩個不同分區的中繼資料加入至分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="fa4b1-216">加入各種不同的索引鍵範圍對應，並顯示分區對應的整體內容。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="fa4b1-217">已撰寫的程式碼讓方法可以在發生錯誤時重新執行。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="fa4b1-218">每個要求會測試是否已經存在分區或對應，然後才嘗試建立。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="fa4b1-219">程式碼假設在字串 **shardServer** 所參考的伺服器中，已建立名為 **sample_shard_0**、**sample_shard_1** 和 **sample_shard_2** 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List the shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="fa4b1-220">或者，您也可以使用 PowerShell 指令碼來達成相同的結果。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="fa4b1-221">部分 PowerShell 範例請見 [這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="fa4b1-222">一旦已填入分區對應，就可建立或調整資料存取應用程式來使用對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="fa4b1-223">除非 **對應配置** 需要變更，否則就不必再次填入或操作對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="fa4b1-224">資料相依路由</span><span class="sxs-lookup"><span data-stu-id="fa4b1-224">Data dependent routing</span></span>
<span data-ttu-id="fa4b1-225">通常是需要資料庫連接來執行應用程式特定資料作業的應用程式，才會使用分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="fa4b1-226">這些連線都必須與正確的資料庫相關聯。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="fa4b1-227">這稱為 **資料相依路由**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="fa4b1-228">對於這些應用程式，請使用對 GSM 資料庫具有唯讀存取的認證，從 Factory 具現化分區對應管理員物件。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="fa4b1-229">稍後連接的個別要求會提供連接到適當分區資料庫所需的認證。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="fa4b1-230">請注意，這些應用程式 (使用以唯讀認證開啟的 **ShardMapManager** ) 將無法變更對應或對應方式。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="fa4b1-231">針對這些需求，請建立管理專用應用程式或 PowerShell 指令碼，以提供稍早所述較高權限的認證。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="fa4b1-232">請參閱 [用來存取彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="fa4b1-233">如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="fa4b1-234">修改分區對應</span><span class="sxs-lookup"><span data-stu-id="fa4b1-234">Modifying a shard map</span></span>
<span data-ttu-id="fa4b1-235">您可以使用不同方式來變更分區對應。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="fa4b1-236">下列所有方法會修改中繼資料 (描述分區和其對應)，但他們不實際修改分區中的資料，也不會建立或刪除實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="fa4b1-237">如下所述，分區對應上的某些作業可能需要與管理動作協調，這些動作會實際移動資料，或是新增和移除資料庫 (做為分區)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="fa4b1-238">這些方法一起做為建置組塊，可用於修改分區化資料庫環境中的整體資料分佈。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="fa4b1-239">若要新增或移除分區：請使用 [Shardmap 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)的 **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** 和 **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="fa4b1-240">代表目標分區的伺服器和資料庫必須存在，才能執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="fa4b1-241">這些方法完全不影響資料庫本身，只影響分區對應中的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="fa4b1-242">若要建立或移除對應至分區的點或範圍：請使用 [RangeShardMapping 類別](https://msdn.microsoft.com/library/azure/dn807318.aspx)的 **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**、**[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**，以及 [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx) 的 **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="fa4b1-243">許多不同的點或範圍可以對應至相同的分區。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="fa4b1-244">這些方法只會影響中繼資料 - 不會影響分區中可能已經存在的任何資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="fa4b1-245">如果需要從資料庫移除資料，才能與 **DeleteMapping** 作業維持一致，您必須另外執行這些作業，但要搭配使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="fa4b1-246">若要將現有的範圍分割成兩個，或將相鄰的範圍合併成一個：請使用 **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** 和 **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="fa4b1-247">請注意，分割及合併作業 **不會變更索引鍵值所對應的分區**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="fa4b1-248">分割會將現有的範圍切割成兩個部分，但會保持兩者都對應至相同的分區。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="fa4b1-249">合併是以兩個已對應至相同分區的相鄰範圍為對象，將它們聯合成單一範圍。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="fa4b1-250">在分區之間移動點或範圍本身時，需要使用 **UpdateMapping** 並配合實際資料移動來協調。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="fa4b1-251">您可以使用彈性資料庫工具的 **分割/合併** 工具，以協調分區對應變更和資料移動 (需要移動時)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="fa4b1-252">若要將個別的點或範圍重新對應 (或移動) 至不同的分區：請使用 **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**的值，連線到正確的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="fa4b1-253">因為資料可能需要從一個分區移至另一個分區，才能與 **UpdateMapping** 作業維持一致，您必須另外執行該動作，但要搭配使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="fa4b1-254">若要讓對應上線和離線︰請使用 **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** 和 **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** 控制對應的線上狀態。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="fa4b1-255">只有當對應處於「離線」狀態時，才允許分區對應上的某些作業，包括 **UpdateMapping** 和 **DeleteMapping**。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="fa4b1-256">對應離線時，根據該對應中包含的索引鍵來提出資料相依要求會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="fa4b1-257">此外，當範圍第一次離線時，受影響分區的所有連線會自動終止，以避免查詢要變更的範圍時產生不一致或不完整的結果。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="fa4b1-258">對應是 .Net 中不可變的物件。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="fa4b1-259">以上會變更對應的所有方法也會使您的程式碼中任何對它們的參考失效。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="fa4b1-260">為了輕鬆執行作業序列來變更對應的狀態，所有會變更對應的方法都會傳回新的對應參考，如此就能鏈結作業。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="fa4b1-261">例如，若要在 shardmap sm 中刪除包含索引鍵 25 的現有對應，您可以執行下列方法：</span><span class="sxs-lookup"><span data-stu-id="fa4b1-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="fa4b1-262">加入分區</span><span class="sxs-lookup"><span data-stu-id="fa4b1-262">Adding a shard</span></span>
<span data-ttu-id="fa4b1-263">對於已經存在的分區對應，應用程式通常只需要加入新的分區，以處理預期來自新的索引鍵或索引鍵範圍的資料。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="fa4b1-264">例如，以租用戶識別碼分區化的應用程式，可能需要為新的租用戶佈建新的分區，或者，每月分區化的資料可能需要在每個新月份開始之前佈建新的分區。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="fa4b1-265">如果索引鍵值的新範圍尚不屬於現有的對應，而且不需要移動任何資料，則加入新的分區並將新的索引鍵或範圍與該分區產生關聯就非常簡單。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="fa4b1-266">如需有關加入新分區的詳細資訊，請參閱 [加入新的分區](sql-database-elastic-scale-add-a-shard.md)。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="fa4b1-267">不過，在需要資料移動的情況下，分割合併工具需要結合必要的分區對應更新，以協調分區之間的資料移動。</span><span class="sxs-lookup"><span data-stu-id="fa4b1-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="fa4b1-268">如需有關使用分割合併工具的詳細資訊，請參閱 [分割合併的概觀](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="fa4b1-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
