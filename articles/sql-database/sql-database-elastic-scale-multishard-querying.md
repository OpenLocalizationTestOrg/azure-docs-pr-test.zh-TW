---
title: "查詢分區化 Azure SQL Database | Microsoft Docs"
description: "使用彈性資料庫用戶端程式跨分區執行查詢。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: 67bcb3c7fe33341103f28bc70e8cc2acbb924cae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="multi-shard-querying"></a><span data-ttu-id="c5f47-103">多分區查詢</span><span class="sxs-lookup"><span data-stu-id="c5f47-103">Multi-shard querying</span></span>
## <a name="overview"></a><span data-ttu-id="c5f47-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c5f47-104">Overview</span></span>
<span data-ttu-id="c5f47-105">使用[彈性資料庫工具](sql-database-elastic-scale-introduction.md)，您可以建立分區化資料庫解決方案。</span><span class="sxs-lookup"><span data-stu-id="c5f47-105">With the [Elastic Database tools](sql-database-elastic-scale-introduction.md), you can create sharded database solutions.</span></span> <span data-ttu-id="c5f47-106">**多分區查詢**用於資料收集/報告等工作，這些工作需要跨越數個分區執行查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f47-106">**Multi-shard querying** is used for tasks such as data collection/reporting that require running a query that stretches across several shards.</span></span> <span data-ttu-id="c5f47-107">(這與在單一分區上執行所有工作的[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)相反。)</span><span class="sxs-lookup"><span data-stu-id="c5f47-107">(Contrast this to [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md), which performs all work on a single shard.)</span></span> 

1. <span data-ttu-id="c5f47-108">使用 [**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)[**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) 或 [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) 方法，取得 [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) 或 [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c5f47-108">Get a [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span> <span data-ttu-id="c5f47-109">請參閱[**建構 ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) 和[**取得 RangeShardMap 或 ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap)。</span><span class="sxs-lookup"><span data-stu-id="c5f47-109">See [**Constructing a ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) and [**Get a RangeShardMap or ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).</span></span>
2. <span data-ttu-id="c5f47-110">建立 **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** 物件。</span><span class="sxs-lookup"><span data-stu-id="c5f47-110">Create a **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** object.</span></span>
3. <span data-ttu-id="c5f47-111">建立 **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="c5f47-111">Create a **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**.</span></span> 
4. <span data-ttu-id="c5f47-112">將 **[CommandText 屬性](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**設定為 T-SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="c5f47-112">Set the **[CommandText property](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)** to a T-SQL command.</span></span>
5. <span data-ttu-id="c5f47-113">呼叫 **[ExecuteReader 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**，以執行命令。</span><span class="sxs-lookup"><span data-stu-id="c5f47-113">Execute the command by calling the **[ExecuteReader method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.</span></span>
6. <span data-ttu-id="c5f47-114">使用 **[MultiShardDataReader 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**，以檢視結果。</span><span class="sxs-lookup"><span data-stu-id="c5f47-114">View the results using the **[MultiShardDataReader class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**.</span></span> 

## <a name="example"></a><span data-ttu-id="c5f47-115">範例</span><span class="sxs-lookup"><span data-stu-id="c5f47-115">Example</span></span>
<span data-ttu-id="c5f47-116">下列程式碼說明如何使用給定的 **ShardMap** (名為 *myShardMap*) 來使用多分區查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f47-116">The following code illustrates the usage of multi-shard querying using a given **ShardMap** named *myShardMap*.</span></span> 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


<span data-ttu-id="c5f47-117">主要差異是多分區連接的建構方式。</span><span class="sxs-lookup"><span data-stu-id="c5f47-117">A key difference is the construction of multi-shard connections.</span></span> <span data-ttu-id="c5f47-118">其中，**SqlConnection** 在單一資料庫上運作，**MultiShardConnection** 接受分區集合做為輸入。</span><span class="sxs-lookup"><span data-stu-id="c5f47-118">Where **SqlConnection** operates on a single database, the **MultiShardConnection** takes a ***collection of shards*** as its input.</span></span> <span data-ttu-id="c5f47-119">從分區對應填入分區集合。</span><span class="sxs-lookup"><span data-stu-id="c5f47-119">Populate the collection of shards from a shard map.</span></span> <span data-ttu-id="c5f47-120">然後，使用 **UNION ALL** 語意在分區集合上執行查詢，以組成單一的整體結果。</span><span class="sxs-lookup"><span data-stu-id="c5f47-120">The query is then executed on the collection of shards using **UNION ALL** semantics to assemble a single overall result.</span></span> <span data-ttu-id="c5f47-121">(選擇性) 在命令上使用 **ExecutionOptions** 屬性，可將資料列的來源分區名稱加入至輸出。</span><span class="sxs-lookup"><span data-stu-id="c5f47-121">Optionally, the name of the shard where the row originates from can be added to the output using the **ExecutionOptions** property on command.</span></span> 

<span data-ttu-id="c5f47-122">請注意 **myShardMap.GetShards()**的呼叫。</span><span class="sxs-lookup"><span data-stu-id="c5f47-122">Note the call to **myShardMap.GetShards()**.</span></span> <span data-ttu-id="c5f47-123">這個方法會從分區對應擷取所有分區，並提供簡單的方式跨所有相關的資料庫執行查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f47-123">This method retrieves all shards from the shard map and provides an easy way to run a query across all relevant databases.</span></span> <span data-ttu-id="c5f47-124">在呼叫 **myShardMap.GetShards()**所傳回的集合分區上執行 LINQ 查詢，可以進一步調整多分區查詢的分區集合。</span><span class="sxs-lookup"><span data-stu-id="c5f47-124">The collection of shards for a multi-shard query can be refined further by performing a LINQ query over the collection returned from the call to **myShardMap.GetShards()**.</span></span> <span data-ttu-id="c5f47-125">結合部分結果原則，多分區查詢目前的功能已設計成可適當處理數十個到數百個分區。</span><span class="sxs-lookup"><span data-stu-id="c5f47-125">In combination with the partial results policy, the current capability in multi-shard querying has been designed to work well for tens up to hundreds of shards.</span></span>

<span data-ttu-id="c5f47-126">多分區查詢目前的限制在於無法驗證所查詢的分區和 Shardlet。</span><span class="sxs-lookup"><span data-stu-id="c5f47-126">A limitation with multi-shard querying is currently the lack of validation for shards and shardlets that are queried.</span></span> <span data-ttu-id="c5f47-127">資料相依路由可在查詢時驗證給定的分區是屬於分區對應，但多分區查詢不會執行這項檢查。</span><span class="sxs-lookup"><span data-stu-id="c5f47-127">While data-dependent routing verifies that a given shard is part of the shard map at the time of querying, multi-shard queries do not perform this check.</span></span> <span data-ttu-id="c5f47-128">這可能會導致在已從分區對應中移除的資料庫上執行多分區查詢。</span><span class="sxs-lookup"><span data-stu-id="c5f47-128">This can lead to multi-shard queries running on databases that have  been removed from the shard map.</span></span>

## <a name="multi-shard-queries-and-split-merge-operations"></a><span data-ttu-id="c5f47-129">多分區查詢與分割合併作業</span><span class="sxs-lookup"><span data-stu-id="c5f47-129">Multi-shard queries and split-merge operations</span></span>
<span data-ttu-id="c5f47-130">多分區查詢不會驗證所查詢資料庫上的 Shardlet 是否參與進行中的分割/合併作業。</span><span class="sxs-lookup"><span data-stu-id="c5f47-130">Multi-shard queries do not verify whether shardlets on the queried database are participating in ongoing split-merge operations.</span></span> <span data-ttu-id="c5f47-131">(請參閱[使用彈性資料庫分割合併工具來縮放](sql-database-elastic-scale-overview-split-and-merge.md)。)這可能會導致不一致的情況，亦即在相同的多分區查詢中，多個資料庫顯示相同 Shardlet 的資料列。</span><span class="sxs-lookup"><span data-stu-id="c5f47-131">(See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).) This can lead to inconsistencies where rows from the same shardlet show for multiple databases in the same multi-shard query.</span></span> <span data-ttu-id="c5f47-132">請注意這些限制，在執行多分區查詢時，請考慮清空進行中的分割/合併作業和分區對應的變更。</span><span class="sxs-lookup"><span data-stu-id="c5f47-132">Be aware of these limitations and consider draining ongoing split-merge operations and changes to the shard map while performing multi-shard queries.</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a><span data-ttu-id="c5f47-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c5f47-133">See also</span></span>
<span data-ttu-id="c5f47-134">**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** 類別和方法。</span><span class="sxs-lookup"><span data-stu-id="c5f47-134">**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** classes and methods.</span></span>

<span data-ttu-id="c5f47-135">使用 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)來管理分區。</span><span class="sxs-lookup"><span data-stu-id="c5f47-135">Manage shards using the [Elastic Database client library](sql-database-elastic-database-client-library.md).</span></span> <span data-ttu-id="c5f47-136">包含稱為 [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) 的命名空間，提供使用單一查詢和結果來查詢多個分區的功能。</span><span class="sxs-lookup"><span data-stu-id="c5f47-136">Includes a  namespace called [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) that provides the ability to query multiple shards using a single query and result.</span></span> <span data-ttu-id="c5f47-137">它提供一組分區的查詢抽象方法。</span><span class="sxs-lookup"><span data-stu-id="c5f47-137">It provides a querying abstraction over a collection of shards.</span></span> <span data-ttu-id="c5f47-138">它也提供替代執行原則，特別是部分結果，以處理查詢許多分區時的失敗。</span><span class="sxs-lookup"><span data-stu-id="c5f47-138">It also provides alternative execution policies, in particular partial results, to deal with failures when querying over many shards.</span></span>  

