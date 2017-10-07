---
title: "分區對應管理員 aaaPerformance 計數器"
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
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a><span data-ttu-id="c1487-103">分區對應管理員的效能計數器</span><span class="sxs-lookup"><span data-stu-id="c1487-103">Performance counters for shard map manager</span></span>
<span data-ttu-id="c1487-104">您可以擷取的 hello 效能[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)，特別是在使用[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="c1487-104">You can capture hello performance of a [shard map manager](sql-database-elastic-scale-shard-map-management.md), especially when using [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="c1487-105">計數器會建立與 hello Microsoft.Azure.SqlDatabase.ElasticScale.Client 類別的方法。</span><span class="sxs-lookup"><span data-stu-id="c1487-105">Counters are created with methods of hello Microsoft.Azure.SqlDatabase.ElasticScale.Client class.</span></span>  

<span data-ttu-id="c1487-106">計數器是使用的 tootrack hello 效能[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)作業。</span><span class="sxs-lookup"><span data-stu-id="c1487-106">Counters are used tootrack hello performance of [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) operations.</span></span> <span data-ttu-id="c1487-107">這些計數器是在 hello 效能監視之下 hello 「 彈性資料庫:: 分區管理 」 類別目錄中存取。</span><span class="sxs-lookup"><span data-stu-id="c1487-107">These counters are accessible in hello Performance Monitor, under hello "Elastic Database: Shard Management" category.</span></span>

<span data-ttu-id="c1487-108">**如需最新版本的 hello:**太移[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="c1487-108">**For hello latest version:** Go too[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> <span data-ttu-id="c1487-109">另請參閱[升級應用程式 toouse hello 最彈性資料庫用戶端程式庫](sql-database-elastic-scale-upgrade-client-library.md)。</span><span class="sxs-lookup"><span data-stu-id="c1487-109">See also [Upgrade an app toouse hello latest elastic database client library](sql-database-elastic-scale-upgrade-client-library.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1487-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="c1487-110">Prerequisites</span></span>
* <span data-ttu-id="c1487-111">hello toocreate hello 效能分類和計數器，使用者必須屬於 hello 本機**管理員**hello 裝載 hello 應用程式的電腦上的群組。</span><span class="sxs-lookup"><span data-stu-id="c1487-111">toocreate hello performance category and counters, hello user must be a part of hello local **Administrators** group on hello machine hosting hello application.</span></span>  
* <span data-ttu-id="c1487-112">toocreate 效能計數器執行個體，然後更新 hello 計數器、 hello 使用者必須屬於其中一個 hello**管理員**或**Performance Monitor Users**群組。</span><span class="sxs-lookup"><span data-stu-id="c1487-112">toocreate a performance counter instance and update hello counters, hello user must be a member of either hello **Administrators** or **Performance Monitor Users** group.</span></span> 

## <a name="create-performance-category-and-counters"></a><span data-ttu-id="c1487-113">建立效能類別和計數器</span><span class="sxs-lookup"><span data-stu-id="c1487-113">Create performance category and counters</span></span>
<span data-ttu-id="c1487-114">toocreate hello 計數器，請呼叫 hello hello CreatePeformanceCategoryAndCounters 方法[ShardMapManagmentFactory 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c1487-114">toocreate hello counters, call hello CreatePeformanceCategoryAndCounters method of hello [ShardMapManagmentFactory class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx).</span></span> <span data-ttu-id="c1487-115">只有系統管理員可以執行 hello 方法：</span><span class="sxs-lookup"><span data-stu-id="c1487-115">Only an administrator can execute hello method:</span></span> 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

<span data-ttu-id="c1487-116">您也可以使用[這](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283)PowerShell 指令碼 tooexecute hello 方法。</span><span class="sxs-lookup"><span data-stu-id="c1487-116">You can also use [this](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) PowerShell script tooexecute hello method.</span></span> <span data-ttu-id="c1487-117">hello 方法會建立下列效能計數器的 hello:</span><span class="sxs-lookup"><span data-stu-id="c1487-117">hello method creates hello following performance counters:</span></span>  

* <span data-ttu-id="c1487-118">**快取對應**: hello 分區對應快取對應的數目。</span><span class="sxs-lookup"><span data-stu-id="c1487-118">**Cached mappings**: Number of mappings cached for hello shard map.</span></span>
* <span data-ttu-id="c1487-119">**DDR 作業數/秒**： 資料依存路由作業 hello 分區對應的速率。</span><span class="sxs-lookup"><span data-stu-id="c1487-119">**DDR operations/sec**: Rate of data dependent routing operations for hello shard map.</span></span> <span data-ttu-id="c1487-120">當呼叫時，會更新這個計數器太[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)導致連線成功 toohello 目的地分區。</span><span class="sxs-lookup"><span data-stu-id="c1487-120">This counter is  updated when a call too[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) results in a successful connection toohello destination shard.</span></span> 
* <span data-ttu-id="c1487-121">**對應查閱快取點擊/秒**: hello 分區對應中對應的成功的快取查閱作業的速率。</span><span class="sxs-lookup"><span data-stu-id="c1487-121">**Mapping lookup cache hits/sec**: Rate of successful cache lookup operations for mappings in hello shard map.</span></span> 
* <span data-ttu-id="c1487-122">**對應查閱快取遺漏數/秒**: hello 分區對應中對應的失敗的快取查閱作業的速率。</span><span class="sxs-lookup"><span data-stu-id="c1487-122">**Mapping lookup cache misses/sec**: Rate of failed cache lookup operations for mappings in hello shard map.</span></span>
* <span data-ttu-id="c1487-123">**對應中新增或更新快取/sec**： 正在加入的對應或 hello 分區對應中更新之快取的速率。</span><span class="sxs-lookup"><span data-stu-id="c1487-123">**Mappings added or updated in cache/sec**: Rate at which mappings are being added or updated in cache for hello shard map.</span></span> 
* <span data-ttu-id="c1487-124">**從快取每秒移除的對應**： 會從快取中的 hello 分區對應移除對應的速率。</span><span class="sxs-lookup"><span data-stu-id="c1487-124">**Mappings removed from cache/sec**: Rate at which mappings are being removed from cache for hello shard map.</span></span> 

<span data-ttu-id="c1487-125">效能計數器會在每個程序針對每個快取的分區對應建立。</span><span class="sxs-lookup"><span data-stu-id="c1487-125">Performance counters are created for each cached shard map per process.</span></span>  

## <a name="notes"></a><span data-ttu-id="c1487-126">注意事項</span><span class="sxs-lookup"><span data-stu-id="c1487-126">Notes</span></span>
<span data-ttu-id="c1487-127">hello 下列事件觸發程序建立 hello hello 效能計數器：</span><span class="sxs-lookup"><span data-stu-id="c1487-127">hello following events trigger hello creation of hello performance counters:</span></span>  

* <span data-ttu-id="c1487-128">初始化 hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)與[積極式載入](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)，如果 hello ShardMapManager 包含任何分區對應。</span><span class="sxs-lookup"><span data-stu-id="c1487-128">Initialization of hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) with [eager loading](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), if hello ShardMapManager contains any shard maps.</span></span> <span data-ttu-id="c1487-129">這些包括 hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29)和 hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="c1487-129">These include hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) and hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) methods.</span></span>
* <span data-ttu-id="c1487-130">成功查閱分區對應 (使用 [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx)、[GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) 或 [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx))。</span><span class="sxs-lookup"><span data-stu-id="c1487-130">Successful lookup of a shard map (using [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) or [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)).</span></span> 
* <span data-ttu-id="c1487-131">使用 CreateShardMap() 成功建立分區對應。</span><span class="sxs-lookup"><span data-stu-id="c1487-131">Successful creation of shard map using CreateShardMap().</span></span>

<span data-ttu-id="c1487-132">hello 分區對應與對應上執行的所有快取作業就會更新 hello 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="c1487-132">hello performance counters will be updated by all cache operations performed on hello shard map and mappings.</span></span> <span data-ttu-id="c1487-133">成功移除刪除的 hello 效能計數器執行個體使用 DeleteShardMap （) reults hello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="c1487-133">Successful removal of hello shard map using DeleteShardMap()reults in deletion of hello performance counters instance.</span></span>  

## <a name="best-practices"></a><span data-ttu-id="c1487-134">最佳作法</span><span class="sxs-lookup"><span data-stu-id="c1487-134">Best practices</span></span>
* <span data-ttu-id="c1487-135">建立 hello 效能分類和計數器，應執行一次 hello ShardMapManager 物件建立之前。</span><span class="sxs-lookup"><span data-stu-id="c1487-135">Creation of hello performance category and counters should be performed only once before hello creation of ShardMapManager object.</span></span> <span data-ttu-id="c1487-136">每次執行 hello 命令 CreatePerformanceCategoryAndCounters() 清除 hello 先前計數器 （遺失所有執行個體所報告的資料），並建立新的。</span><span class="sxs-lookup"><span data-stu-id="c1487-136">Every execution of hello command CreatePerformanceCategoryAndCounters() clears hello previous counters (losing data reported by all instances) and creates new ones.</span></span>  
* <span data-ttu-id="c1487-137">每個程序都會建立效能計數器執行個體。</span><span class="sxs-lookup"><span data-stu-id="c1487-137">Performance counter instances are created per process.</span></span> <span data-ttu-id="c1487-138">任何應用程式損毀或移除分區對應從 hello 快取會導致刪除 hello 效能計數器執行個體。</span><span class="sxs-lookup"><span data-stu-id="c1487-138">Any application crash or removal of a shard map from hello cache will result in deletion of hello performance counters instances.</span></span>  

### <a name="see-also"></a><span data-ttu-id="c1487-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c1487-139">See also</span></span>
[<span data-ttu-id="c1487-140">彈性資料庫功能概觀</span><span class="sxs-lookup"><span data-stu-id="c1487-140">Elastic Database features overview</span></span>](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

