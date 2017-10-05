---
title: "彈性資料庫工具字彙 | Microsoft Docs"
description: "彈性資料庫工具所用詞彙的解釋"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="35d57-103">彈性資料庫工具字彙</span><span class="sxs-lookup"><span data-stu-id="35d57-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="35d57-104">下列詞彙是針對 [彈性資料庫工具](sql-database-elastic-scale-introduction.md)(Azure SQL Database的一項功能) 所定義的。</span><span class="sxs-lookup"><span data-stu-id="35d57-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="35d57-105">這些工具是用來管理[分區對應](sql-database-elastic-scale-shard-map-management.md)，並且包含[用戶端程式庫](sql-database-elastic-database-client-library.md)、[分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)、[彈性集區](sql-database-elastic-pool.md)及[查詢](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="35d57-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="35d57-106">在[使用彈性資料庫工具加入分區](sql-database-elastic-scale-add-a-shard.md)和[使用 RecoveryManager 類別來修正分區對應問題](sql-database-elastic-database-recovery-manager.md)中會用到這些詞彙。</span><span class="sxs-lookup"><span data-stu-id="35d57-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![彈性擴縮詞彙][1]

<span data-ttu-id="35d57-108">**資料庫**：Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="35d57-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="35d57-109">**資料依存路由**：可讓應用程式根據特定的分區化索引鍵連接到分區的功能。</span><span class="sxs-lookup"><span data-stu-id="35d57-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="35d57-110">請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="35d57-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="35d57-111">請對照 **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**。</span><span class="sxs-lookup"><span data-stu-id="35d57-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="35d57-112">**全域分區對應**：在**分區集**之內，分區化索引鍵及其個別分區之間的對應。</span><span class="sxs-lookup"><span data-stu-id="35d57-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="35d57-113">全域分區對應儲存在 **分區對應管理員**中。</span><span class="sxs-lookup"><span data-stu-id="35d57-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="35d57-114">請對照 **本機分區對應**。</span><span class="sxs-lookup"><span data-stu-id="35d57-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="35d57-115">**清單分區對應**：逐一對應分區化索引鍵的分區對應。</span><span class="sxs-lookup"><span data-stu-id="35d57-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="35d57-116">請對照 **範圍分區對應**。</span><span class="sxs-lookup"><span data-stu-id="35d57-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="35d57-117">**本機分區對應**：儲存在分區上的本機分區對應包含位於分區上之 Shardlet 的對應。</span><span class="sxs-lookup"><span data-stu-id="35d57-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="35d57-118">**多分區查詢**：能夠對多個分區發出查詢，使用 UNION ALL 語意傳回結果集 (也稱為「展開傳送查詢」)。</span><span class="sxs-lookup"><span data-stu-id="35d57-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="35d57-119">請對照 **資料相依路由**。</span><span class="sxs-lookup"><span data-stu-id="35d57-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="35d57-120">**多租用戶**和**單一租用戶**︰這會顯示單一租用戶資料庫和多租用戶資料庫︰</span><span class="sxs-lookup"><span data-stu-id="35d57-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![單一和多租用戶資料庫](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="35d57-122">以下是 **分區化** 單一和多租用戶資料庫的呈現。</span><span class="sxs-lookup"><span data-stu-id="35d57-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![單一和多租用戶資料庫](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="35d57-124">**範圍分區對應**：根據多個連續值範圍來制訂分區分佈策略的分區對應。</span><span class="sxs-lookup"><span data-stu-id="35d57-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="35d57-125">**參考資料表**：不分區化而是跨分區複寫的資料表。</span><span class="sxs-lookup"><span data-stu-id="35d57-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="35d57-126">例如，郵遞區號可以儲存參考資料表中。</span><span class="sxs-lookup"><span data-stu-id="35d57-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="35d57-127">**分區**：儲存來自分區化資料集之資料的 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="35d57-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="35d57-128">**分區彈性**：能夠執行**水平縮放**與**垂直縮放**。</span><span class="sxs-lookup"><span data-stu-id="35d57-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="35d57-129">**分區化資料表**：分區化的資料表，亦即，資料根據其分區化索引鍵值而分佈至分區。</span><span class="sxs-lookup"><span data-stu-id="35d57-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="35d57-130">**分區化索引鍵**：決定資料如何分佈至分區的資料行值。</span><span class="sxs-lookup"><span data-stu-id="35d57-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="35d57-131">值類型可以是下列其中一個：**int**、**bigint**、**varbinary** 或 **uniqueidentifier**。</span><span class="sxs-lookup"><span data-stu-id="35d57-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="35d57-132">**分區集**：在分區對應管理員中屬於相同分區對應的分區集合。</span><span class="sxs-lookup"><span data-stu-id="35d57-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="35d57-133">**Shardlet**：與分區上之分區化索引鍵的單一值相關聯的所有資料。</span><span class="sxs-lookup"><span data-stu-id="35d57-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="35d57-134">在重新分佈分區化資料表時，Shardlet 是可能的資料移動最小單位。</span><span class="sxs-lookup"><span data-stu-id="35d57-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="35d57-135">**分區對應**：分區化索引鍵和其個別分區之間的對應集合。</span><span class="sxs-lookup"><span data-stu-id="35d57-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="35d57-136">**分區對應管理員**：管理物件和資料存放區，其中包含分區對應、分區位置，以及一或多個分區集的對應。</span><span class="sxs-lookup"><span data-stu-id="35d57-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![對應][2]

## <a name="verbs"></a><span data-ttu-id="35d57-138">動詞</span><span class="sxs-lookup"><span data-stu-id="35d57-138">Verbs</span></span>
<span data-ttu-id="35d57-139">**水平縮放**：藉由在分區對應中新增或移除分區而相應放大 (或縮小) 分區集合的動作，如下所示。</span><span class="sxs-lookup"><span data-stu-id="35d57-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![水平和垂直縮放][3]

<span data-ttu-id="35d57-141">**合併**：將兩個分區的 Shardlet 移至一個分區並相應地更新分區對應的動作。</span><span class="sxs-lookup"><span data-stu-id="35d57-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="35d57-142">**Shardlet 移動**：將單一 Shardlet 移至不同分區的動作。</span><span class="sxs-lookup"><span data-stu-id="35d57-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="35d57-143">**分區**：根據分區化索引鍵將結構完全相同的資料水平分割至多個資料庫的動作。</span><span class="sxs-lookup"><span data-stu-id="35d57-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="35d57-144">**分割**：將一個分區的數個 Shardlet 移至另一個 (通常是新的) 分區的動作。</span><span class="sxs-lookup"><span data-stu-id="35d57-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="35d57-145">使用者提供分區化金鑰做為分割點。</span><span class="sxs-lookup"><span data-stu-id="35d57-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="35d57-146">**垂直縮放**：相應增加 (或減少) 個別分區之效能層級的動作。</span><span class="sxs-lookup"><span data-stu-id="35d57-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="35d57-147">例如，將分區從 Standard 變更為 Premium (獲得更多計算資源)。</span><span class="sxs-lookup"><span data-stu-id="35d57-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

