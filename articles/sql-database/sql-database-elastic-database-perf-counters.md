---
title: "分區對應管理員的效能計數器"
description: "ShardMapManager 類別與資料相依路由效能計數器"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: 60bb26fe6833998137ede71b363d5d40479a4c60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="performance-counters-for-shard-map-manager"></a><span data-ttu-id="485b2-103">分區對應管理員的效能計數器</span><span class="sxs-lookup"><span data-stu-id="485b2-103">Performance counters for shard map manager</span></span>
<span data-ttu-id="485b2-104">您可以擷取[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)的效能，特別是在使用[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)時。</span><span class="sxs-lookup"><span data-stu-id="485b2-104">You can capture the performance of a [shard map manager](sql-database-elastic-scale-shard-map-management.md), especially when using [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="485b2-105">計數器是使用 Microsoft.Azure.SqlDatabase.ElasticScale.Client 類別的方法建立。</span><span class="sxs-lookup"><span data-stu-id="485b2-105">Counters are created with methods of the Microsoft.Azure.SqlDatabase.ElasticScale.Client class.</span></span>  

<span data-ttu-id="485b2-106">計數器是用來追蹤 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md) 作業的效能。</span><span class="sxs-lookup"><span data-stu-id="485b2-106">Counters are used to track the performance of [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) operations.</span></span> <span data-ttu-id="485b2-107">這些計數器可在「彈性資料庫：分區管理」類別下的「效能監視器」中存取。</span><span class="sxs-lookup"><span data-stu-id="485b2-107">These counters are accessible in the Performance Monitor, under the "Elastic Database: Shard Management" category.</span></span>

<span data-ttu-id="485b2-108">**如需最新版本** ：請瀏覽 [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="485b2-108">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> <span data-ttu-id="485b2-109">另請參閱 [將應用程式升級以使用最新的彈性資料庫用戶端程式庫](sql-database-elastic-scale-upgrade-client-library.md)。</span><span class="sxs-lookup"><span data-stu-id="485b2-109">See also [Upgrade an app to use the latest elastic database client library](sql-database-elastic-scale-upgrade-client-library.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="485b2-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="485b2-110">Prerequisites</span></span>
* <span data-ttu-id="485b2-111">若要建立效能類別和計數器，使用者必須屬於裝載應用程式的電腦上的本機 **Administrators** 群組。</span><span class="sxs-lookup"><span data-stu-id="485b2-111">To create the performance category and counters, the user must be a part of the local **Administrators** group on the machine hosting the application.</span></span>  
* <span data-ttu-id="485b2-112">若要建立效能計數器執行個體和更新計數器，使用者必須是 **Administrators** 或 **Performance Monitor Users** 群組的成員。</span><span class="sxs-lookup"><span data-stu-id="485b2-112">To create a performance counter instance and update the counters, the user must be a member of either the **Administrators** or **Performance Monitor Users** group.</span></span> 

## <a name="create-performance-category-and-counters"></a><span data-ttu-id="485b2-113">建立效能類別和計數器</span><span class="sxs-lookup"><span data-stu-id="485b2-113">Create performance category and counters</span></span>
<span data-ttu-id="485b2-114">若要建立計數器，請呼叫 [ShardMapManagmentFactory 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx)的 CreatePeformanceCategoryAndCounters 方法。</span><span class="sxs-lookup"><span data-stu-id="485b2-114">To create the counters, call the CreatePeformanceCategoryAndCounters method of the [ShardMapManagmentFactory class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx).</span></span> <span data-ttu-id="485b2-115">只有系統管理員可以執行這個方法︰</span><span class="sxs-lookup"><span data-stu-id="485b2-115">Only an administrator can execute the method:</span></span> 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

<span data-ttu-id="485b2-116">您也可以使用 [這個](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell 指令碼來執行方法。</span><span class="sxs-lookup"><span data-stu-id="485b2-116">You can also use [this](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell script to execute the method.</span></span> <span data-ttu-id="485b2-117">這個方法會建立下列效能計數器︰</span><span class="sxs-lookup"><span data-stu-id="485b2-117">The method creates the following performance counters:</span></span>  

* <span data-ttu-id="485b2-118">**快取對應**︰針對分區對應快取的對應數目。</span><span class="sxs-lookup"><span data-stu-id="485b2-118">**Cached mappings**: Number of mappings cached for the shard map.</span></span>
* <span data-ttu-id="485b2-119">**DDR 作業數/秒**︰分區對應的資料相依路由作業速率。</span><span class="sxs-lookup"><span data-stu-id="485b2-119">**DDR operations/sec**: Rate of data dependent routing operations for the shard map.</span></span> <span data-ttu-id="485b2-120">對 [OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) 的呼叫導致順利連接到目的地分區時，就會更新此計數器。</span><span class="sxs-lookup"><span data-stu-id="485b2-120">This counter is  updated when a call to [OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) results in a successful connection to the destination shard.</span></span> 
* <span data-ttu-id="485b2-121">**對應查閱快取點擊/秒**︰分區對應中對應的成功快取查閱作業的速率。</span><span class="sxs-lookup"><span data-stu-id="485b2-121">**Mapping lookup cache hits/sec**: Rate of successful cache lookup operations for mappings in the shard map.</span></span> 
* <span data-ttu-id="485b2-122">**對應查閱快取遺失/秒**︰分區對應中對應的失敗快取查閱作業的速率。</span><span class="sxs-lookup"><span data-stu-id="485b2-122">**Mapping lookup cache misses/sec**: Rate of failed cache lookup operations for mappings in the shard map.</span></span>
* <span data-ttu-id="485b2-123">**快取中的對應新增或更新/秒**︰分區對應的快取中新增或更新對應的速率。</span><span class="sxs-lookup"><span data-stu-id="485b2-123">**Mappings added or updated in cache/sec**: Rate at which mappings are being added or updated in cache for the shard map.</span></span> 
* <span data-ttu-id="485b2-124">**從快取中移除對應/秒**︰從分區對應的快取中移除對應的速率。</span><span class="sxs-lookup"><span data-stu-id="485b2-124">**Mappings removed from cache/sec**: Rate at which mappings are being removed from cache for the shard map.</span></span> 

<span data-ttu-id="485b2-125">效能計數器會在每個程序針對每個快取的分區對應建立。</span><span class="sxs-lookup"><span data-stu-id="485b2-125">Performance counters are created for each cached shard map per process.</span></span>  

## <a name="notes"></a><span data-ttu-id="485b2-126">注意事項</span><span class="sxs-lookup"><span data-stu-id="485b2-126">Notes</span></span>
<span data-ttu-id="485b2-127">下列事件會觸發效能計數器的建立︰</span><span class="sxs-lookup"><span data-stu-id="485b2-127">The following events trigger the creation of the performance counters:</span></span>  

* <span data-ttu-id="485b2-128">在 ShardMapManager 包含任何分區對應的情況下，使用[積極式載入](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)將 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 初始化。</span><span class="sxs-lookup"><span data-stu-id="485b2-128">Initialization of the [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) with [eager loading](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), if the ShardMapManager contains any shard maps.</span></span> <span data-ttu-id="485b2-129">這些包括 [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) 和 [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="485b2-129">These include the [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) and the [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) methods.</span></span>
* <span data-ttu-id="485b2-130">成功查閱分區對應 (使用 [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx)、[GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) 或 [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx))。</span><span class="sxs-lookup"><span data-stu-id="485b2-130">Successful lookup of a shard map (using [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) or [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)).</span></span> 
* <span data-ttu-id="485b2-131">使用 CreateShardMap() 成功建立分區對應。</span><span class="sxs-lookup"><span data-stu-id="485b2-131">Successful creation of shard map using CreateShardMap().</span></span>

<span data-ttu-id="485b2-132">效能計數器會由分區對應和對應上執行的所有快取作業更新。</span><span class="sxs-lookup"><span data-stu-id="485b2-132">The performance counters will be updated by all cache operations performed on the shard map and mappings.</span></span> <span data-ttu-id="485b2-133">使用 DeleteShardMap() 導致刪除效能計數器執行個體，成功移除分區對應。</span><span class="sxs-lookup"><span data-stu-id="485b2-133">Successful removal of the shard map using DeleteShardMap()reults in deletion of the performance counters instance.</span></span>  

## <a name="best-practices"></a><span data-ttu-id="485b2-134">最佳作法</span><span class="sxs-lookup"><span data-stu-id="485b2-134">Best practices</span></span>
* <span data-ttu-id="485b2-135">建立效能類別和計數器應該僅在建立 ShardMapManager 物件之前執行一次。</span><span class="sxs-lookup"><span data-stu-id="485b2-135">Creation of the performance category and counters should be performed only once before the creation of ShardMapManager object.</span></span> <span data-ttu-id="485b2-136">每次執行命令 CreatePerformanceCategoryAndCounters() 都會清除先前的計數器 (遺失所有執行個體報告的資料)，並建立新的計數器。</span><span class="sxs-lookup"><span data-stu-id="485b2-136">Every execution of the command CreatePerformanceCategoryAndCounters() clears the previous counters (losing data reported by all instances) and creates new ones.</span></span>  
* <span data-ttu-id="485b2-137">每個程序都會建立效能計數器執行個體。</span><span class="sxs-lookup"><span data-stu-id="485b2-137">Performance counter instances are created per process.</span></span> <span data-ttu-id="485b2-138">任何應用程式當機或從快取移除分區對應都會導致刪除效能計數器執行個體。</span><span class="sxs-lookup"><span data-stu-id="485b2-138">Any application crash or removal of a shard map from the cache will result in deletion of the performance counters instances.</span></span>  

### <a name="see-also"></a><span data-ttu-id="485b2-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="485b2-139">See also</span></span>
[<span data-ttu-id="485b2-140">彈性資料庫功能概觀</span><span class="sxs-lookup"><span data-stu-id="485b2-140">Elastic Database features overview</span></span>](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

