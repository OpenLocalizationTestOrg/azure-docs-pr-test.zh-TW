---
title: "aaaElastic 資料庫工具詞彙 |Microsoft 文件"
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="3ec6a-103">彈性資料庫工具字彙</span><span class="sxs-lookup"><span data-stu-id="3ec6a-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="3ec6a-104">hello 下列所定義的詞彙 hello[彈性資料庫工具](sql-database-elastic-scale-introduction.md)，Azure SQL Database 的功能。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="3ec6a-105">hello 工具會使用的 toomanage[分區對應](sql-database-elastic-scale-shard-map-management.md)，並包含 hello[用戶端程式庫](sql-database-elastic-database-client-library.md)，hello[分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)，[彈性集區](sql-database-elastic-pool.md)，和[查詢](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="3ec6a-106">這些授權條款會以[新增分區使用彈性資料庫工具](sql-database-elastic-scale-add-a-shard.md)和[使用 hello RecoveryManager 類別 toofix 分區對應問題](sql-database-elastic-database-recovery-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![彈性擴縮詞彙][1]

<span data-ttu-id="3ec6a-108">**資料庫**：Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="3ec6a-109">**資料依存路由**: hello 功能，可提供特定的分區化索引鍵的應用程式 tooconnect tooa 分區。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="3ec6a-110">請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="3ec6a-111">比較太**[多分區查詢](sql-database-elastic-scale-multishard-querying.md)**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="3ec6a-112">**全域分區對應**: hello 之間分區化索引鍵和其各自的分區間進行對應**分區集**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="3ec6a-113">hello 全域分區對應會儲存在 hello**分區對應管理員**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="3ec6a-114">比較太**本機分區對應**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="3ec6a-115">**清單分區對應**：逐一對應分區化索引鍵的分區對應。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="3ec6a-116">比較太**範圍分區對應**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="3ec6a-117">**本機分區對應**： 儲存於分區，hello 本機分區對應包含 hello shardlet 位於 hello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="3ec6a-118">**多個分區查詢**: hello 能力 tooissue 針對多個分區的查詢，則會傳回結果集，使用 UNION ALL 語意 （也稱為 「 展開傳送查詢 」）。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="3ec6a-119">比較太**資料依存路由**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="3ec6a-120">**多租用戶**和**單一租用戶**︰這會顯示單一租用戶資料庫和多租用戶資料庫︰</span><span class="sxs-lookup"><span data-stu-id="3ec6a-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![單一和多租用戶資料庫](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="3ec6a-122">以下是 **分區化** 單一和多租用戶資料庫的呈現。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![單一和多租用戶資料庫](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="3ec6a-124">**範圍分區對應**： 分區對應中的 hello 分區散發策略根據多個連續值的範圍。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="3ec6a-125">**參考資料表**：不分區化而是跨分區複寫的資料表。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="3ec6a-126">例如，郵遞區號可以儲存參考資料表中。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="3ec6a-127">**分區**：儲存來自分區化資料集之資料的 Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="3ec6a-128">**分區彈性**: hello 能力 tooperform**水平延展**和**垂直縮放比例**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="3ec6a-129">**分區化資料表**：分區化的資料表，亦即，資料根據其分區化索引鍵值而分佈至分區。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="3ec6a-130">**分區化索引鍵**：決定資料如何分佈至分區的資料行值。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="3ec6a-131">hello 實值型別可以是 hello 下列其中一種： **int**， **bigint**， **varbinary**，或**uniqueidentifier**。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="3ec6a-132">**分區集**: hello 的屬性化的 toohello 的分區集合 hello 分區對應管理員中的相同分區對應。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="3ec6a-133">**Shardlet**： 所有 hello 與單一值的分區有分區化索引鍵相關聯的資料。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="3ec6a-134">Shardlet 時轉散發分區化資料表的資料移動可能 hello 最小單位。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="3ec6a-135">**分區對應**: hello 的分區化索引鍵和其個別分區之間的對應集合。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="3ec6a-136">**分區對應管理員**: hello 分區 map(s)、 分區位置，以及對應的一或多個分區集包含為管理物件和資料存放區。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![對應][2]

## <a name="verbs"></a><span data-ttu-id="3ec6a-138">動詞</span><span class="sxs-lookup"><span data-stu-id="3ec6a-138">Verbs</span></span>
<span data-ttu-id="3ec6a-139">**水平延展**: hello act 的縮放比例外 （或） 的新增或移除分區 tooa 分區對應，如下所示的分區集合。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![水平和垂直縮放][3]

<span data-ttu-id="3ec6a-141">**合併**: hello 動作從兩個分區 tooone 分區移動 shardlet 並據以更新 hello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="3ec6a-142">**Shardlet 移動**: hello 動作 tooa 不同單一 shardlet 的分區。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="3ec6a-143">**分區**： 跨多個資料庫分區化索引鍵為基礎的水平資料分割具有相同的 hello 動作結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="3ec6a-144">**分割**: hello act 從一個分區 tooanother （通常是新的） 分區移幾個 shardlet。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="3ec6a-145">分區化索引鍵是由 hello 使用者提供，如 hello 分割點。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="3ec6a-146">**垂直縮放比例**: hello act 縮放 （上下） 的 hello 個別分區效能層級。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="3ec6a-147">例如，變更分區從標準 tooPremium （這會導致更多運算資源）。</span><span class="sxs-lookup"><span data-stu-id="3ec6a-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

