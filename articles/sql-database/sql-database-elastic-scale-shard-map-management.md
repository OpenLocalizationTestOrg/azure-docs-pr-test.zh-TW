---
title: "Azure SQL database 出 aaaScale |Microsoft 文件"
description: "如何 toouse hello ShardMapManager，彈性資料庫用戶端程式庫"
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
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="a284a-103">擴充資料庫與 hello 分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="a284a-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="a284a-104">tooeasily 向外延展資料庫的 SQL Azure 使用分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="a284a-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="a284a-105">hello 分區對應管理員是一個特殊的資料庫維護分區集中的所有分區 （資料庫） 的通用對應資訊。</span><span class="sxs-lookup"><span data-stu-id="a284a-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="a284a-106">hello 中繼資料可讓應用程式 tooconnect toohello 正確的資料庫為基礎的 hello hello 值**分區化索引鍵**。</span><span class="sxs-lookup"><span data-stu-id="a284a-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="a284a-107">此外，每個分區集中 hello 包含追蹤 hello 本機分區資料的對應 (稱為**shardlet**)。</span><span class="sxs-lookup"><span data-stu-id="a284a-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![分區對應管理](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="a284a-109">了解如何建構這些對應是不可或缺的 tooshard 對應管理。</span><span class="sxs-lookup"><span data-stu-id="a284a-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="a284a-110">這是使用 hello [ShardMapManager 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)，找到在 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)toomanage 分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="a284a-111">分區對應和分區對應方式</span><span class="sxs-lookup"><span data-stu-id="a284a-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="a284a-112">對於每個分區，您必須選取分區對應 toocreate hello 型別。</span><span class="sxs-lookup"><span data-stu-id="a284a-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="a284a-113">hello 選擇取決於 hello 資料庫架構：</span><span class="sxs-lookup"><span data-stu-id="a284a-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="a284a-114">每個資料庫的單一租用戶</span><span class="sxs-lookup"><span data-stu-id="a284a-114">Single tenant per database</span></span>  
2. <span data-ttu-id="a284a-115">每個資料庫的多個租用戶 (兩種類型)︰</span><span class="sxs-lookup"><span data-stu-id="a284a-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="a284a-116">清單對應</span><span class="sxs-lookup"><span data-stu-id="a284a-116">List mapping</span></span>
   2. <span data-ttu-id="a284a-117">範圍對應</span><span class="sxs-lookup"><span data-stu-id="a284a-117">Range mapping</span></span>

<span data-ttu-id="a284a-118">針對單一租用戶模型，建立 **清單對應** 分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="a284a-119">hello 單一租用戶模型會指派一個資料庫，每個租用戶。</span><span class="sxs-lookup"><span data-stu-id="a284a-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="a284a-120">這是適用於 SaaS 開發人員的有效模式，因為它會簡化管理。</span><span class="sxs-lookup"><span data-stu-id="a284a-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![清單對應][1]

<span data-ttu-id="a284a-122">hello 多租用戶模型會指派數個租用戶 tooa 單一資料庫 （和分散多個資料庫的租用戶的群組）。</span><span class="sxs-lookup"><span data-stu-id="a284a-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="a284a-123">當您希望產生每個租用戶 toohave 小型資料需要使用此模型。</span><span class="sxs-lookup"><span data-stu-id="a284a-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="a284a-124">在此模型中，我們會將指派租用戶 tooa 資料庫使用的範圍**範圍對應**。</span><span class="sxs-lookup"><span data-stu-id="a284a-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![範圍對應][2]

<span data-ttu-id="a284a-126">您可以實作多租用戶資料庫模型，使用或*清單對應*tooassign 多個租用戶 tooa 單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="a284a-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="a284a-127">例如，DB1 是租用戶識別碼 1 和 5，請使用的 toostore 的資訊，而 DB2 儲存 7 租用戶和租用戶 10 的資料。</span><span class="sxs-lookup"><span data-stu-id="a284a-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![單一資料庫上的多個租用戶][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="a284a-129">分區化索引鍵支援的 .Net 型別</span><span class="sxs-lookup"><span data-stu-id="a284a-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="a284a-130">彈性延展支援 hello 下列.Net Framework 類型為分區化索引鍵：</span><span class="sxs-lookup"><span data-stu-id="a284a-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="a284a-131">integer</span><span class="sxs-lookup"><span data-stu-id="a284a-131">integer</span></span>
* <span data-ttu-id="a284a-132">long</span><span class="sxs-lookup"><span data-stu-id="a284a-132">long</span></span>
* <span data-ttu-id="a284a-133">guid</span><span class="sxs-lookup"><span data-stu-id="a284a-133">guid</span></span>
* <span data-ttu-id="a284a-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="a284a-134">byte[]</span></span>  
* <span data-ttu-id="a284a-135">datetime</span><span class="sxs-lookup"><span data-stu-id="a284a-135">datetime</span></span>
* <span data-ttu-id="a284a-136">timespan</span><span class="sxs-lookup"><span data-stu-id="a284a-136">timespan</span></span>
* <span data-ttu-id="a284a-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a284a-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="a284a-138">清單和範圍分區對應</span><span class="sxs-lookup"><span data-stu-id="a284a-138">List and range shard maps</span></span>
<span data-ttu-id="a284a-139">建構分區對應時可以選擇使用**個別分區化索引鍵值的清單**，或使用**分區化索引鍵值的範圍**。</span><span class="sxs-lookup"><span data-stu-id="a284a-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="a284a-140">清單分區對應</span><span class="sxs-lookup"><span data-stu-id="a284a-140">List shard maps</span></span>
<span data-ttu-id="a284a-141">**分區**包含**shardlet** ，shardlet tooshards hello 對應也維持分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="a284a-142">A**清單分區對應**hello 個別索引鍵值，找出 hello shardlet 與 hello 資料庫做為分區之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="a284a-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="a284a-143">**列出對應**會明確且不同的索引鍵的值可以是對應的 toohello 相同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a284a-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="a284a-144">例如，索引鍵為 1 對應 tooDatabase A 並 3 到 6 的索引鍵值參考資料庫 b。</span><span class="sxs-lookup"><span data-stu-id="a284a-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="a284a-145">Key</span><span class="sxs-lookup"><span data-stu-id="a284a-145">Key</span></span> | <span data-ttu-id="a284a-146">分區位置</span><span class="sxs-lookup"><span data-stu-id="a284a-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="a284a-147">1</span><span class="sxs-lookup"><span data-stu-id="a284a-147">1</span></span> |<span data-ttu-id="a284a-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="a284a-148">Database_A</span></span> |
| <span data-ttu-id="a284a-149">3</span><span class="sxs-lookup"><span data-stu-id="a284a-149">3</span></span> |<span data-ttu-id="a284a-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="a284a-150">Database_B</span></span> |
| <span data-ttu-id="a284a-151">4</span><span class="sxs-lookup"><span data-stu-id="a284a-151">4</span></span> |<span data-ttu-id="a284a-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="a284a-152">Database_C</span></span> |
| <span data-ttu-id="a284a-153">6</span><span class="sxs-lookup"><span data-stu-id="a284a-153">6</span></span> |<span data-ttu-id="a284a-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="a284a-154">Database_B</span></span> |
| <span data-ttu-id="a284a-155">...</span><span class="sxs-lookup"><span data-stu-id="a284a-155">...</span></span> |<span data-ttu-id="a284a-156">...</span><span class="sxs-lookup"><span data-stu-id="a284a-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="a284a-157">範圍分區對應</span><span class="sxs-lookup"><span data-stu-id="a284a-157">Range shard maps</span></span>
<span data-ttu-id="a284a-158">在**範圍分區對應**，由一組描述 hello 索引鍵範圍**[低值、 最高值）**其中 hello*低值*hello hello 範圍和 hello中的最小金鑰*高價值*是 hello 高於 hello 範圍的第一個值。</span><span class="sxs-lookup"><span data-stu-id="a284a-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="a284a-159">例如，**[0, 100)** 包含所有大於或等於 0 且小於 100 的整數。</span><span class="sxs-lookup"><span data-stu-id="a284a-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="a284a-160">請注意，支援多個範圍可以點 toohello 相同資料庫，以及脫離的範圍 (例如，[100200) 和 [400,600) 這兩個點 tooDatabase C hello 下面範例中。)</span><span class="sxs-lookup"><span data-stu-id="a284a-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="a284a-161">Key</span><span class="sxs-lookup"><span data-stu-id="a284a-161">Key</span></span> | <span data-ttu-id="a284a-162">分區位置</span><span class="sxs-lookup"><span data-stu-id="a284a-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="a284a-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="a284a-163">[1,50)</span></span> |<span data-ttu-id="a284a-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="a284a-164">Database_A</span></span> |
| <span data-ttu-id="a284a-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="a284a-165">[50,100)</span></span> |<span data-ttu-id="a284a-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="a284a-166">Database_B</span></span> |
| <span data-ttu-id="a284a-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="a284a-167">[100,200)</span></span> |<span data-ttu-id="a284a-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="a284a-168">Database_C</span></span> |
| <span data-ttu-id="a284a-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="a284a-169">[400,600)</span></span> |<span data-ttu-id="a284a-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="a284a-170">Database_C</span></span> |
| <span data-ttu-id="a284a-171">...</span><span class="sxs-lookup"><span data-stu-id="a284a-171">...</span></span> |<span data-ttu-id="a284a-172">...</span><span class="sxs-lookup"><span data-stu-id="a284a-172">...</span></span> |

<span data-ttu-id="a284a-173">如上所示的 hello 資料表的每一個都是一個概念的範例**ShardMap**物件。</span><span class="sxs-lookup"><span data-stu-id="a284a-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="a284a-174">每個資料列是個人的簡化的範例**PointMapping** （適用於 hello 清單分區對應） 或**RangeMapping** （適用於 hello 範圍分區對應） 物件。</span><span class="sxs-lookup"><span data-stu-id="a284a-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="a284a-175">分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="a284a-175">Shard map manager</span></span>
<span data-ttu-id="a284a-176">Hello 用戶端程式庫，hello 分區對應管理員是分區對應的集合。</span><span class="sxs-lookup"><span data-stu-id="a284a-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="a284a-177">hello 所管理的資料**ShardMapManager**執行個體就會保留在三個位置：</span><span class="sxs-lookup"><span data-stu-id="a284a-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="a284a-178">**全域分區對應 (GSM)**： 您指定資料庫 tooserve 為 hello 所有分區對應及對應的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="a284a-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="a284a-179">特殊的資料表和預存程序會自動建立 toomanage hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="a284a-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="a284a-180">這通常是一個小型資料庫，以及少量的存取，並不應該使用 hello 應用程式的其他需求。</span><span class="sxs-lookup"><span data-stu-id="a284a-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="a284a-181">hello 資料表是在特殊結構描述中名為**__ShardManagement**。</span><span class="sxs-lookup"><span data-stu-id="a284a-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="a284a-182">**分區對應 (LSM)**： 您指定的 toobe 分區是修改 toocontain，數個小型資料表和包含與管理分區對應資訊的特定 toothat 分區的特殊預存程序的每個資料庫。</span><span class="sxs-lookup"><span data-stu-id="a284a-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="a284a-183">這項資訊是與 hello GSM 中的 hello 資訊多餘的它允許 hello 應用程式快取 toovalidate 分區對應資訊而不在 hello GSM; 中放置任何負載hello 應用程式會使用 hello LSM toodetermine，如果快取的對應仍然有效。</span><span class="sxs-lookup"><span data-stu-id="a284a-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="a284a-184">hello 資料表上每個分區 LSM 還有 hello 結構描述中的對應 toohello **__ShardManagement**。</span><span class="sxs-lookup"><span data-stu-id="a284a-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="a284a-185">**應用程式快取**：每個存取 **ShardMapManager** 物件的應用程式執行個體會維護其對應的本機記憶體內部快取。</span><span class="sxs-lookup"><span data-stu-id="a284a-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="a284a-186">它會儲存最近擷取的路由資訊。</span><span class="sxs-lookup"><span data-stu-id="a284a-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="a284a-187">建構 ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="a284a-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="a284a-188">**ShardMapManager** 物件是使用 [Factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) 模式所建構。</span><span class="sxs-lookup"><span data-stu-id="a284a-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="a284a-189">hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** 方法採用 hello 形式的認證 （包括 hello 伺服器名稱和資料庫名稱保留 hello GSM） **ConnectionString**和傳回的執行個體**ShardMapManager**。</span><span class="sxs-lookup"><span data-stu-id="a284a-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="a284a-190">**請注意：** hello **ShardMapManager**應該具現化一次只能每個應用程式的 hello 初始化程式碼內的應用程式網域。</span><span class="sxs-lookup"><span data-stu-id="a284a-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="a284a-191">建立額外的執行個體的 ShardMapManager hello 中相同的 appdomain 中，會導致增加的記憶體和 CPU 的使用率 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a284a-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="a284a-192">**ShardMapManager** 可以包含任意數目的分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="a284a-193">雖然單一分區對應可能足夠用於許多應用程式，但有時幾組不同的資料庫會用於不同的結構描述或做為特殊用途；在這些情況下，最好使用多個分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="a284a-194">在這段程式碼，應用程式會嘗試在現有 tooopen **ShardMapManager**以 hello [TryGetSqlShardMapManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a284a-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="a284a-195">如果物件，代表全域**ShardMapManager** (GSM) 不相符，尚未存在 hello 資料庫內，hello 用戶端程式庫會建立它們那里使用 hello [CreateSqlShardMapManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a284a-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
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
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="a284a-196">或者，您可以使用 Powershell toocreate 新的分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="a284a-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="a284a-197">範例請見 [這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="a284a-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="a284a-198">取得 RangeShardMap 或 ListShardMap</span><span class="sxs-lookup"><span data-stu-id="a284a-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="a284a-199">在建立之後分區對應管理員，您可以取得 hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx)或[ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx)使用 hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)，hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)，或使用 hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="a284a-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="a284a-200">分區對應系統管理認證</span><span class="sxs-lookup"><span data-stu-id="a284a-200">Shard map administration credentials</span></span>
<span data-ttu-id="a284a-201">管理和操作分區對應的應用程式會不同於使用 hello 分區對應 tooroute 連線。</span><span class="sxs-lookup"><span data-stu-id="a284a-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="a284a-202">tooadminister 分區對應 （新增或變更分區，分區對應中，分區對應等） 必須具現化 hello **ShardMapManager**使用**認證具有讀取/寫入權限，這兩個 hello GSM 資料庫上與每個做為分區化資料庫**。</span><span class="sxs-lookup"><span data-stu-id="a284a-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="a284a-203">hello 認證必須允許針對這兩個 hello 中的 hello 資料表寫入 GSM 和 LSM 分區對應資訊是輸入或變更，以及與建立新的分區 LSM 資料表時。</span><span class="sxs-lookup"><span data-stu-id="a284a-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="a284a-204">請參閱[使用 tooaccess hello 彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="a284a-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="a284a-205">只影響中繼資料</span><span class="sxs-lookup"><span data-stu-id="a284a-205">Only metadata affected</span></span>
<span data-ttu-id="a284a-206">用於填入或變更 hello 方法**ShardMapManager**資料不會改變 hello 使用者資料儲存在本身的 hello 分區中。</span><span class="sxs-lookup"><span data-stu-id="a284a-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="a284a-207">比方說，這類方法**CreateShard**， **DeleteShard**， **UpdateMapping**等影響 hello 分區對應僅為中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a284a-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="a284a-208">請勿移除、 新增或變更包含在 hello 分區中的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="a284a-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="a284a-209">相反地，這些方法是使用設計的 toobe 搭配不同的作業執行 toocreate 或移除實際的資料庫，或該移動的資料列從一個分區 tooanother toorebalance 分區化的環境。</span><span class="sxs-lookup"><span data-stu-id="a284a-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="a284a-210">(hello**分割合併**彈性資料庫工具所隨附的工具會使用這些 Api，以及協調分區之間的實際資料移動。)請參閱[調整使用 hello 彈性資料庫分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)。</span><span class="sxs-lookup"><span data-stu-id="a284a-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="a284a-211">填入分區對應範例</span><span class="sxs-lookup"><span data-stu-id="a284a-211">Populating a shard map example</span></span>
<span data-ttu-id="a284a-212">作業 toopopulate 特定分區對應的範例順序如下所示。</span><span class="sxs-lookup"><span data-stu-id="a284a-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="a284a-213">hello 程式碼執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a284a-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="a284a-214">在分區對應管理員內建立新的分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="a284a-215">兩個不同分區的 hello 中繼資料會加入 toohello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="a284a-216">加入各種不同的索引鍵範圍的對應，並 hello 整體 hello 分區對應會顯示的內容。</span><span class="sxs-lookup"><span data-stu-id="a284a-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="a284a-217">hello 程式碼會寫入，以便可以重新執行 hello 方法，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a284a-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="a284a-218">每個要求會測試是否分區或對應已經存在，然後再嘗試 toocreate 它。</span><span class="sxs-lookup"><span data-stu-id="a284a-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="a284a-219">hello 程式碼會假設資料庫命名為**sample_shard_0**， **sample_shard_1**和**sample_shard_2** hello 字串所參考的伺服器中已經建立**shardServer**。</span><span class="sxs-lookup"><span data-stu-id="a284a-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

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

            // List hello shards and mappings 
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

<span data-ttu-id="a284a-220">因為替代，您可以使用 PowerShell 指令碼 tooachieve hello 結果相同。</span><span class="sxs-lookup"><span data-stu-id="a284a-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="a284a-221">有些 hello 範例 PowerShell 範例[這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。</span><span class="sxs-lookup"><span data-stu-id="a284a-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="a284a-222">一旦填入分區對應之後，資料存取應用程式可以建立，或調整 toowork 與 hello 地圖。</span><span class="sxs-lookup"><span data-stu-id="a284a-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="a284a-223">填入或操作 hello 對應需要不會發生一次，直到**對應配置**需要 toochange。</span><span class="sxs-lookup"><span data-stu-id="a284a-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="a284a-224">資料相依路由</span><span class="sxs-lookup"><span data-stu-id="a284a-224">Data dependent routing</span></span>
<span data-ttu-id="a284a-225">hello 分區對應管理員將最用於需要資料庫連接 tooperform hello 應用程式特定資料作業的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a284a-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="a284a-226">這些連線必須與 hello 正確的資料庫相關聯。</span><span class="sxs-lookup"><span data-stu-id="a284a-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="a284a-227">這稱為 **資料相依路由**。</span><span class="sxs-lookup"><span data-stu-id="a284a-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="a284a-228">對於這些應用程式中，具現化 hello 原廠使用 hello GSM 資料庫具有唯讀存取權的認證從分區對應管理員物件。</span><span class="sxs-lookup"><span data-stu-id="a284a-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="a284a-229">個別的更新版本的連線要求提供連線 toohello 適當的分區化資料庫所需的認證。</span><span class="sxs-lookup"><span data-stu-id="a284a-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="a284a-230">請注意，這些應用程式 (使用**ShardMapManager**開啟具有唯讀的認證) toohello 對應的無法進行變更。</span><span class="sxs-lookup"><span data-stu-id="a284a-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="a284a-231">針對這些需求，請建立管理專用應用程式或 PowerShell 指令碼，以提供稍早所述較高權限的認證。</span><span class="sxs-lookup"><span data-stu-id="a284a-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="a284a-232">請參閱[使用 tooaccess hello 彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="a284a-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="a284a-233">如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="a284a-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="a284a-234">修改分區對應</span><span class="sxs-lookup"><span data-stu-id="a284a-234">Modifying a shard map</span></span>
<span data-ttu-id="a284a-235">您可以使用不同方式來變更分區對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="a284a-236">所有 hello 下列方法修改 hello 中繼資料描述 hello 分區和他們的對應，但他們不實際修改 hello 分區內的資料也請勿在建立或刪除 hello 實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a284a-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="a284a-237">某些 hello hello 分區對應如下所述的作業可能需要 toobe 協調的實際移動資料，或者加入和移除資料庫做為分區的系統管理動作。</span><span class="sxs-lookup"><span data-stu-id="a284a-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="a284a-238">這些方法一起當作 hello 建置組塊可用於修改 hello 整體分佈的分區化資料庫環境中的資料。</span><span class="sxs-lookup"><span data-stu-id="a284a-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="a284a-239">tooadd 或移除分區： 使用 **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** 和 **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** 的 hello [Shardmap 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a284a-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="a284a-240">hello 伺服器和資料庫代表 hello 目標分區必須已經存在的這些作業 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="a284a-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="a284a-241">這些方法只能在 hello 分區對應中的中繼資料本身，hello 資料庫上沒有任何影響。</span><span class="sxs-lookup"><span data-stu-id="a284a-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="a284a-242">對應 toohello 分區 toocreate 或移除點或範圍： 使用 **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**，  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** 的 hello[RangeShardMapping 類別](https://msdn.microsoft.com/library/azure/dn807318.aspx)，和 **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** 的 hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="a284a-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="a284a-243">許多不同時間點或範圍可以對應的 toohello 相同分區。</span><span class="sxs-lookup"><span data-stu-id="a284a-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="a284a-244">這些方法只會影響中繼資料 - 不會影響分區中可能已經存在的任何資料。</span><span class="sxs-lookup"><span data-stu-id="a284a-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="a284a-245">如果資料需要從 hello 中順序 toobe 與一致的資料庫中移除的 toobe **DeleteMapping**作業，您將需要 tooperform 這些作業分別但搭配使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="a284a-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="a284a-246">toosplit 兩種、 或合併成一個相鄰的範圍到現有的範圍： 使用 **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** 和 **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="a284a-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="a284a-247">請注意，分割及合併作業**不會變更 hello 分區 toowhich 機碼值會對應**。</span><span class="sxs-lookup"><span data-stu-id="a284a-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="a284a-248">分割的現有範圍分成兩個部分，但會保留兩種形式對應 toohello 相同分區。</span><span class="sxs-lookup"><span data-stu-id="a284a-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="a284a-249">已對應的 toohello 的兩個相鄰範圍上運作的合併相同的分區，聯合它們成單一範圍。</span><span class="sxs-lookup"><span data-stu-id="a284a-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="a284a-250">hello 的點或分區之間本身範圍移動需要 toobe 協調使用**UpdateMapping**搭配實際的資料移動。</span><span class="sxs-lookup"><span data-stu-id="a284a-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="a284a-251">您可以使用 hello**分割/合併**屬於彈性資料庫的服務需要移動時，工具 toocoordinate 分區對應變更的資料移動。</span><span class="sxs-lookup"><span data-stu-id="a284a-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="a284a-252">toore 對應 （或移動） 個別點或範圍 toodifferent 分區： 使用 **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="a284a-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="a284a-253">因為資料可能需要從一個分區 tooanother 中與一致的順序 toobe 移 toobe **UpdateMapping**作業，您將需要 tooperform 該移動分開但搭配使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="a284a-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="a284a-254">線上和離線 tootake 對應： 使用 **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** 和 **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello 的線上狀態對應。</span><span class="sxs-lookup"><span data-stu-id="a284a-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="a284a-255">只有當對應處於「離線」狀態時，才允許分區對應上的某些作業，包括 **UpdateMapping** 和 **DeleteMapping**。</span><span class="sxs-lookup"><span data-stu-id="a284a-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="a284a-256">對應離線時，根據該對應中包含的索引鍵來提出資料相依要求會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="a284a-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="a284a-257">此外，範圍第一次離線時，所有連線 toohello 影響分區會自動都終止順序 tooprevent 不一致或不完整結果的查詢，針對要變更的範圍中。</span><span class="sxs-lookup"><span data-stu-id="a284a-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="a284a-258">對應是 .Net 中不可變的物件。</span><span class="sxs-lookup"><span data-stu-id="a284a-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="a284a-259">Hello 上述方法，變更對應的所有也會使程式碼中的任何參考 toothem。</span><span class="sxs-lookup"><span data-stu-id="a284a-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="a284a-260">toomake it 更容易 tooperform 順序的變更對應的狀態，變更對應的 hello 方法的所有作業都會傳回新對應的參考，讓作業可以鏈結。</span><span class="sxs-lookup"><span data-stu-id="a284a-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="a284a-261">比方說，現有的對應中包含 hello 金鑰 25 shardmap sm toodelete，您可以執行下列的 hello:</span><span class="sxs-lookup"><span data-stu-id="a284a-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="a284a-262">加入分區</span><span class="sxs-lookup"><span data-stu-id="a284a-262">Adding a shard</span></span>
<span data-ttu-id="a284a-263">應用程式通常需要 toosimply 新增分區 toohandle 資料應從新的索引鍵或索引鍵範圍，分區對應已經存在。</span><span class="sxs-lookup"><span data-stu-id="a284a-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="a284a-264">比方說，分區化應用程式的租用戶識別碼可能需要 tooprovision 新的分區，新的租用戶，或資料分區化每月可能需要新的分區，佈建的每個新月份的 hello 起始之前。</span><span class="sxs-lookup"><span data-stu-id="a284a-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="a284a-265">如果 hello 新索引鍵值的範圍還不屬於現有的對應並不會移動資料是必要的它是非常簡單 tooadd hello 新的分區，並將 hello 新的金鑰或範圍 toothat 分區產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a284a-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="a284a-266">如需有關加入新分區的詳細資訊，請參閱 [加入新的分區](sql-database-elastic-scale-add-a-shard.md)。</span><span class="sxs-lookup"><span data-stu-id="a284a-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="a284a-267">不過，需要移動資料的情況下，hello 分割合併工具是分區搭配 hello 必要分區對應更新之間的所需的 tooorchestrate hello 資料移動。</span><span class="sxs-lookup"><span data-stu-id="a284a-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="a284a-268">如需使用詳細資訊 hello yool 分割合併，請參閱 <<c0> [ 分割合併的概觀](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="a284a-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
