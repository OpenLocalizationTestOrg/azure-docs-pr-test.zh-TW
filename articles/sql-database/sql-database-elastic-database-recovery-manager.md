---
title: "aaaUsing 復原管理員 toofix 分區對應問題 |Microsoft 文件"
description: "使用 hello RecoveryManager 類別 toosolve 問題分區對應"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a><span data-ttu-id="129e4-103">使用 hello RecoveryManager 類別 toofix 分區對應問題</span><span class="sxs-lookup"><span data-stu-id="129e4-103">Using hello RecoveryManager class toofix shard map problems</span></span>
<span data-ttu-id="129e4-104">hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx)類別提供 hello 能力 tooeasily 偵測並修正任何不一致性 hello 全域分區對應 (GSM) 與分區化資料庫環境中的 hello 本機分區對應 (LSM) 之間的 ADO.Net 應用程式。</span><span class="sxs-lookup"><span data-stu-id="129e4-104">hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) class provides ADO.Net applications hello ability tooeasily detect and correct any inconsistencies between hello global shard map (GSM) and hello local shard map (LSM) in a sharded database environment.</span></span> 

<span data-ttu-id="129e4-105">hello GSM 和 LSM 追蹤 hello 對應之每個資料庫分區化的環境中。</span><span class="sxs-lookup"><span data-stu-id="129e4-105">hello GSM and LSM track hello mapping of each database in a sharded environment.</span></span> <span data-ttu-id="129e4-106">有時候，hello GSM 與 hello LSM 之間發生中斷。</span><span class="sxs-lookup"><span data-stu-id="129e4-106">Occasionally, a break occurs between hello GSM and hello LSM.</span></span> <span data-ttu-id="129e4-107">在此情況下，使用 hello RecoveryManager 類別 toodetect 並修復 hello 中斷。</span><span class="sxs-lookup"><span data-stu-id="129e4-107">In that case, use hello RecoveryManager class toodetect and repair hello break.</span></span>

<span data-ttu-id="129e4-108">hello RecoveryManager 類別屬於 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-108">hello RecoveryManager class is part of hello [Elastic Database client library](sql-database-elastic-database-client-library.md).</span></span> 

![分區對應][1]

<span data-ttu-id="129e4-110">關於詞彙定義，請參閱 [彈性資料庫工具字彙](sql-database-elastic-scale-glossary.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-110">For term definitions, see [Elastic Database tools glossary](sql-database-elastic-scale-glossary.md).</span></span> <span data-ttu-id="129e4-111">如何 hello toounderstand **ShardMapManager**使用的 toomanage 資料在分區化解決方案中，請參閱[分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-111">toounderstand how hello **ShardMapManager** is used toomanage data in a sharded solution, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span>

## <a name="why-use-hello-recovery-manager"></a><span data-ttu-id="129e4-112">為何要使用 hello 復原管理員？</span><span class="sxs-lookup"><span data-stu-id="129e4-112">Why use hello recovery manager?</span></span>
<span data-ttu-id="129e4-113">在分區化資料庫環境中，每個資料庫有一個租用戶，而每個伺服器中有許多資料庫。</span><span class="sxs-lookup"><span data-stu-id="129e4-113">In a sharded database environment, there is one tenant per database, and many databases per server.</span></span> <span data-ttu-id="129e4-114">可以也有許多伺服器 hello 環境中。</span><span class="sxs-lookup"><span data-stu-id="129e4-114">There can also be many servers in hello environment.</span></span> <span data-ttu-id="129e4-115">每個資料庫會在 hello 分區對應中，對應，以便呼叫能夠路由的 toohello 正確的伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="129e4-115">Each database is mapped in hello shard map, so calls can be routed toohello correct server and database.</span></span> <span data-ttu-id="129e4-116">資料庫會追蹤根據 tooa**分區化索引鍵**，並指派每個分區**鍵值範圍**。</span><span class="sxs-lookup"><span data-stu-id="129e4-116">Databases are tracked according tooa **sharding key**, and each shard is assigned a **range of key values**.</span></span> <span data-ttu-id="129e4-117">例如，分區化索引鍵可能代表 hello 客戶名稱從"D"太"F.的"</span><span class="sxs-lookup"><span data-stu-id="129e4-117">For example, a sharding key may represent hello customer names from "D" too"F."</span></span> <span data-ttu-id="129e4-118">hello 所有分區 （也稱為資料庫） 的對應，而且其對應的範圍會包含在 hello**全域分區對應 (GSM)**。</span><span class="sxs-lookup"><span data-stu-id="129e4-118">hello mapping of all shards (aka databases) and their mapping ranges are contained in hello **global shard map (GSM)**.</span></span> <span data-ttu-id="129e4-119">每個資料庫也包含的 hello 範圍包含在 hello 就所謂的 hello 分區對應**本機分區對應 (LSM)**。</span><span class="sxs-lookup"><span data-stu-id="129e4-119">Each database also contains a map of hello ranges contained on hello shard that is known as hello **local shard map (LSM)**.</span></span> <span data-ttu-id="129e4-120">當應用程式連接 tooa 分區時，快速擷取 hello 應用程式快取 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-120">When an app connects tooa shard, hello mapping is cached with hello app for quick retrieval.</span></span> <span data-ttu-id="129e4-121">hello LSM 是使用的 toovalidate 快取資料。</span><span class="sxs-lookup"><span data-stu-id="129e4-121">hello LSM is used toovalidate cached data.</span></span> 

<span data-ttu-id="129e4-122">hello GSM 和 LSM 變得不同步的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="129e4-122">hello GSM and LSM may become out of sync for hello following reasons:</span></span>

1. <span data-ttu-id="129e4-123">分區，其範圍相信 toono 較長的 hello 刪除作業會使用或重新命名的分區中。</span><span class="sxs-lookup"><span data-stu-id="129e4-123">hello deletion of a shard whose range is believed toono longer be in use, or renaming of a shard.</span></span> <span data-ttu-id="129e4-124">刪除分區會導致 **被遺棄的分區對應**。</span><span class="sxs-lookup"><span data-stu-id="129e4-124">Deleting a shard results in an **orphaned shard mapping**.</span></span> <span data-ttu-id="129e4-125">同樣地，重新命名的資料庫可能造成被遺棄的分區對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-125">Similarly, a renamed database can cause an orphaned shard mapping.</span></span> <span data-ttu-id="129e4-126">根據 hello 的 hello 變更的意圖，hello 分區可能需要移除 toobe 或 hello 分區位置需要 toobe 更新。</span><span class="sxs-lookup"><span data-stu-id="129e4-126">Depending on hello intent of hello change, hello shard may need toobe removed or hello shard location needs toobe updated.</span></span> <span data-ttu-id="129e4-127">toorecover 已刪除的資料庫，請參閱[還原已刪除的資料庫](sql-database-recovery-using-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-127">toorecover a deleted database, see [Restore a deleted database](sql-database-recovery-using-backups.md).</span></span>
2. <span data-ttu-id="129e4-128">發生異地備援容錯移轉事件。</span><span class="sxs-lookup"><span data-stu-id="129e4-128">A geo-failover event occurs.</span></span> <span data-ttu-id="129e4-129">toocontinue，一個必須更新 hello 伺服器名稱及分區對應中的所有分區分區對應管理員 hello 應用程式，然後更新 hello 分區對應詳細資料的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="129e4-129">toocontinue, one must update hello server name, and database name of shard map manager in hello application and then update hello shard mapping details for all shards in a shard map.</span></span> <span data-ttu-id="129e4-130">地理容錯移轉時，應該自動化這類復原邏輯 hello 容錯移轉工作流程內。</span><span class="sxs-lookup"><span data-stu-id="129e4-130">If there is a geo-failover, such recovery logic should be automated within hello failover workflow.</span></span> <span data-ttu-id="129e4-131">自動化修復動作可為異地備援的資料庫啟用順暢的管理能力，並避免人工的動作。</span><span class="sxs-lookup"><span data-stu-id="129e4-131">Automating recovery actions enables a frictionless manageability for geo-enabled databases and avoids manual human actions.</span></span> <span data-ttu-id="129e4-132">關於資料庫是否有資料中心中斷，請參閱選項 toorecover toolearn[業務續航力](sql-database-business-continuity.md)和[嚴重損壞修復](sql-database-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-132">toolearn about options toorecover a database if there is a data center outage, see [Business Continuity](sql-database-business-continuity.md) and [Disaster Recovery](sql-database-disaster-recovery.md).</span></span>
3. <span data-ttu-id="129e4-133">分區或 hello ShardMapManager 資料庫會還原的 tooan 稍早的點的時間。</span><span class="sxs-lookup"><span data-stu-id="129e4-133">Either a shard or hello ShardMapManager database is restored tooan earlier point-in time.</span></span> <span data-ttu-id="129e4-134">toolearn 相關時間點復原使用備份，請參閱[使用備份復原](sql-database-recovery-using-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-134">toolearn about point in time recovery using backups, see [Recovery using backups](sql-database-recovery-using-backups.md).</span></span>

<span data-ttu-id="129e4-135">如需有關 Azure SQL Database 彈性資料庫工具、 地理複寫和還原的詳細資訊，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="129e4-135">For more information about Azure SQL Database Elastic Database tools, geo-replication and Restore, see hello following:</span></span> 

* [<span data-ttu-id="129e4-136">概觀：雲端商務持續性和 SQL Database 的資料庫災害復原</span><span class="sxs-lookup"><span data-stu-id="129e4-136">Overview: Cloud business continuity and database disaster recovery with SQL Database</span></span>](sql-database-business-continuity.md) 
* [<span data-ttu-id="129e4-137">開始使用彈性資料庫工具</span><span class="sxs-lookup"><span data-stu-id="129e4-137">Get started with elastic database tools</span></span>](sql-database-elastic-scale-get-started.md)  
* [<span data-ttu-id="129e4-138">ShardMap 管理</span><span class="sxs-lookup"><span data-stu-id="129e4-138">ShardMap Management</span></span>](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a><span data-ttu-id="129e4-139">從 ShardMapManager 擷取 RecoveryManager</span><span class="sxs-lookup"><span data-stu-id="129e4-139">Retrieving RecoveryManager from a ShardMapManager</span></span>
<span data-ttu-id="129e4-140">hello 第一個步驟是 toocreate RecoveryManager 執行個體。</span><span class="sxs-lookup"><span data-stu-id="129e4-140">hello first step is toocreate a RecoveryManager instance.</span></span> <span data-ttu-id="129e4-141">hello [GetRecoveryManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx)傳回 hello hello 目前復原管理員[ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)執行個體。</span><span class="sxs-lookup"><span data-stu-id="129e4-141">hello [GetRecoveryManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) returns hello recovery manager for hello current [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) instance.</span></span> <span data-ttu-id="129e4-142">將對應 tooaddress hello 分區中的不一致，您必須先擷取 hello RecoveryManager hello 特定分區對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-142">tooaddress any inconsistencies in hello shard map, you must first retrieve hello RecoveryManager for hello particular shard map.</span></span> 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

<span data-ttu-id="129e4-143">在此範例中，會從 hello ShardMapManager hello RecoveryManager 組初始化。</span><span class="sxs-lookup"><span data-stu-id="129e4-143">In this example, hello RecoveryManager is initialized from hello ShardMapManager.</span></span> <span data-ttu-id="129e4-144">hello ShardMapManager 包含 ShardMap 也已經初始化。</span><span class="sxs-lookup"><span data-stu-id="129e4-144">hello ShardMapManager containing a ShardMap is also already initialized.</span></span> 

<span data-ttu-id="129e4-145">因為此應用程式程式碼操作 hello 分區對應本身，hello hello factory 方法中使用的認證 (在上述範例中，hello smmConnectionString) 應該是具有 hello 所參考的 hello GSM 資料庫讀寫權限的認證連接字串。</span><span class="sxs-lookup"><span data-stu-id="129e4-145">Since this application code manipulates hello shard map itself, hello credentials used in hello factory method (in hello preceding example, smmConnectionString) should be credentials that have read-write permissions on hello GSM database referenced by hello connection string.</span></span> <span data-ttu-id="129e4-146">這些認證所用認證 tooopen 連線資料依存路由通常不同。</span><span class="sxs-lookup"><span data-stu-id="129e4-146">These credentials are typically different from credentials used tooopen connections for data-dependent routing.</span></span> <span data-ttu-id="129e4-147">如需詳細資訊，請參閱[hello 彈性資料庫用戶端中使用認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-147">For more information, see [Using credentials in hello elastic database client](sql-database-elastic-scale-manage-credentials.md).</span></span>

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a><span data-ttu-id="129e4-148">從 hello ShardMap 移除分區之後會刪除分區</span><span class="sxs-lookup"><span data-stu-id="129e4-148">Removing a shard from hello ShardMap after a shard is deleted</span></span>
<span data-ttu-id="129e4-149">hello [DetachShard 方法](https://msdn.microsoft.com/library/azure/dn842083.aspx)卸離 hello 根據分區指定 hello 分區對應，並刪除 hello 分區相關聯的對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-149">hello [DetachShard method](https://msdn.microsoft.com/library/azure/dn842083.aspx) detaches hello given shard from hello shard map and deletes mappings associated with hello shard.</span></span>  

* <span data-ttu-id="129e4-150">hello 分區位置，特別是伺服器名稱和資料庫名稱，要卸離的 hello 分區 hello 位置參數。</span><span class="sxs-lookup"><span data-stu-id="129e4-150">hello location parameter is hello shard location, specifically server name and database name, of hello shard being detached.</span></span> 
* <span data-ttu-id="129e4-151">hello shardMapName 參數是 hello 分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="129e4-151">hello shardMapName parameter is hello shard map name.</span></span> <span data-ttu-id="129e4-152">這只是需要： 當多個分區對應由 hello 相同分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="129e4-152">This is only required when multiple shard maps are managed by hello same shard map manager.</span></span> <span data-ttu-id="129e4-153">選用。</span><span class="sxs-lookup"><span data-stu-id="129e4-153">Optional.</span></span> 


> [!IMPORTANT]
> <span data-ttu-id="129e4-154">只有在特定 hello 更新對應的 hello 範圍是空的請使用這項技術。</span><span class="sxs-lookup"><span data-stu-id="129e4-154">Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span> <span data-ttu-id="129e4-155">上述的 hello 方法不會檢查正在移動的 hello 範圍的資料，因此最適合 tooinclude 會檢查您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="129e4-155">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>
>

<span data-ttu-id="129e4-156">這個範例會移除 hello 分區對應中的分區。</span><span class="sxs-lookup"><span data-stu-id="129e4-156">This example removes shards from hello shard map.</span></span> 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

<span data-ttu-id="129e4-157">hello 分區對應會反映在 hello GSM hello 分區的 hello 刪除之前的 hello 分區位置。</span><span class="sxs-lookup"><span data-stu-id="129e4-157">hello shard map reflects hello shard location in hello GSM before hello deletion of hello shard.</span></span> <span data-ttu-id="129e4-158">因為已刪除 hello 分區，它會假設這是有意的且 hello 分區化索引鍵範圍不再使用中。</span><span class="sxs-lookup"><span data-stu-id="129e4-158">Because hello shard was deleted, it is assumed this was intentional, and hello sharding key range is no longer in use.</span></span> <span data-ttu-id="129e4-159">如果情況並非如此，您可以執行時間點還原，</span><span class="sxs-lookup"><span data-stu-id="129e4-159">If not, you can execute point-in time restore.</span></span> <span data-ttu-id="129e4-160">toorecover hello 分區從較早的時間點。</span><span class="sxs-lookup"><span data-stu-id="129e4-160">toorecover hello shard from an earlier point-in-time.</span></span> <span data-ttu-id="129e4-161">（在此情況下，檢閱下列區段 toodetect 分區不一致的 hello）。toorecover，請參閱[時間點復原](sql-database-recovery-using-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="129e4-161">(In that case, review hello following section toodetect shard inconsistencies.) toorecover, see [Point in time recovery](sql-database-recovery-using-backups.md).</span></span>

<span data-ttu-id="129e4-162">因為它假設 hello 資料庫刪除有意，hello 最終的系統管理清理動作是 toodelete hello 項目 toohello 分區 hello 分區對應管理員中。</span><span class="sxs-lookup"><span data-stu-id="129e4-162">Since it is assumed hello database deletion was intentional, hello final administrative cleanup action is toodelete hello entry toohello shard in hello shard map manager.</span></span> <span data-ttu-id="129e4-163">這可避免不慎撰寫未預期的資訊 tooa 範圍 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="129e4-163">This prevents hello application from inadvertently writing information tooa range that is not expected.</span></span>

## <a name="toodetect-mapping-differences"></a><span data-ttu-id="129e4-164">toodetect 對應的差異</span><span class="sxs-lookup"><span data-stu-id="129e4-164">toodetect mapping differences</span></span>
<span data-ttu-id="129e4-165">hello [DetectMappingDifferences 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx)選取並傳回 hello 分區對應 （本機或全域） 的其中一個為 hello 事實來源調解 （GSM 和 LSM） 這兩個分區對應上的對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-165">hello [DetectMappingDifferences method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) selects and returns one of hello shard maps (either local or global) as hello source of truth and reconciles mappings on both shard maps (GSM and LSM).</span></span>

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* <span data-ttu-id="129e4-166">hello*位置*指定 hello 伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="129e4-166">hello *location* specifies hello server name and database name.</span></span> 
* <span data-ttu-id="129e4-167">hello *shardMapName*參數是 hello 分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="129e4-167">hello *shardMapName* parameter is hello shard map name.</span></span> <span data-ttu-id="129e4-168">這只是需要多個分區對應的 hello 都受相同的分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="129e4-168">This is only required if multiple shard maps are managed by hello same shard map manager.</span></span> <span data-ttu-id="129e4-169">選用。</span><span class="sxs-lookup"><span data-stu-id="129e4-169">Optional.</span></span> 

## <a name="tooresolve-mapping-differences"></a><span data-ttu-id="129e4-170">tooresolve 對應的差異</span><span class="sxs-lookup"><span data-stu-id="129e4-170">tooresolve mapping differences</span></span>
<span data-ttu-id="129e4-171">hello [ResolveMappingDifferences 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx)為 hello 事實來源中選取一個 hello 分區對應 （本機或全域） 並調解 （GSM 和 LSM） 這兩個分區對應上的對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-171">hello [ResolveMappingDifferences method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) selects one of hello shard maps (either local or global) as hello source of truth and reconciles mappings on both shard maps (GSM and LSM).</span></span>

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* <span data-ttu-id="129e4-172">hello *RecoveryToken*參數列舉 hello 對應 hello GSM 之間 hello LSM hello 特定分區的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="129e4-172">hello *RecoveryToken* parameter enumerates hello differences in hello mappings between hello GSM and hello LSM for hello specific shard.</span></span> 
* <span data-ttu-id="129e4-173">hello [MappingDifferenceResolution 列舉](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx)是使用的 tooindicate hello 方法來解析 hello hello 分區對應的差異。</span><span class="sxs-lookup"><span data-stu-id="129e4-173">hello [MappingDifferenceResolution enumeration](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) is used tooindicate hello method for resolving hello difference between hello shard mappings.</span></span> 
* <span data-ttu-id="129e4-174">**MappingDifferenceResolution.KeepShardMapping**時，建議的 hello LSM 包含 hello 精確對應，因此應該使用 hello 分區中的 hello 對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-174">**MappingDifferenceResolution.KeepShardMapping** is recommended that when hello LSM contains hello accurate mapping and therefore hello mapping in hello shard should be used.</span></span> <span data-ttu-id="129e4-175">這是通常 hello 情況下，如果容錯移轉： hello 分區現在位於新的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="129e4-175">This is typically hello case if there is a failover: hello shard now resides on a new server.</span></span> <span data-ttu-id="129e4-176">因為從 hello GSM （使用 hello RecoveryManager.DetachShard 方法） 時，您必須先移除 hello 分區，其對應不再存在 hello GSM 上。</span><span class="sxs-lookup"><span data-stu-id="129e4-176">Since hello shard must first be removed from hello GSM (using hello RecoveryManager.DetachShard method), a mapping no longer exists on hello GSM.</span></span> <span data-ttu-id="129e4-177">因此，hello LSM 必須使用的 toore-建立 hello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-177">Therefore, hello LSM must be used toore-establish hello shard mapping.</span></span>

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a><span data-ttu-id="129e4-178">附加分區 toohello ShardMap 分區還原之後</span><span class="sxs-lookup"><span data-stu-id="129e4-178">Attach a shard toohello ShardMap after a shard is restored</span></span>
<span data-ttu-id="129e4-179">hello [AttachShard 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx)附加 hello 給定的分區 toohello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-179">hello [AttachShard method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) attaches hello given shard toohello shard map.</span></span> <span data-ttu-id="129e4-180">然後會偵測任何分區對應不一致，並更新 hello 對應 toomatch hello 分區 hello hello 分區還原點。</span><span class="sxs-lookup"><span data-stu-id="129e4-180">It then detects any shard map inconsistencies and updates hello mappings toomatch hello shard at hello point of hello shard restoration.</span></span> <span data-ttu-id="129e4-181">它會假設該 hello 資料庫也是重新命名的 tooreflect hello 原始資料庫名稱 （之前已還原 hello 分區），因為 hello 時間點還原預設值 tooa hello 時間戳記附加新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="129e4-181">It is assumed that hello database is also renamed tooreflect hello original database name (before hello shard was restored), since hello point-in time restoration defaults tooa new database appended with hello timestamp.</span></span> 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* <span data-ttu-id="129e4-182">hello*位置*參數是 hello 伺服器名稱和資料庫名稱，要附加的 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="129e4-182">hello *location* parameter is hello server name and database name, of hello shard being attached.</span></span> 
* <span data-ttu-id="129e4-183">hello *shardMapName*參數是 hello 分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="129e4-183">hello *shardMapName* parameter is hello shard map name.</span></span> <span data-ttu-id="129e4-184">這只是需要： 當多個分區對應由 hello 相同分區對應管理員。</span><span class="sxs-lookup"><span data-stu-id="129e4-184">This is only required when multiple shard maps are managed by hello same shard map manager.</span></span> <span data-ttu-id="129e4-185">選用。</span><span class="sxs-lookup"><span data-stu-id="129e4-185">Optional.</span></span> 

<span data-ttu-id="129e4-186">這個範例會將已經從較早的中點時間最近還原分區 toohello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-186">This example adds a shard toohello shard map that has been recently restored from an earlier point-in time.</span></span> <span data-ttu-id="129e4-187">Hello 分區 (也就是在 hello LSM hello 分區對應的 hello) 已還原，因為它是與 hello GSM 中的 hello 分區項目可能不一致。</span><span class="sxs-lookup"><span data-stu-id="129e4-187">Since hello shard (namely hello mapping for hello shard in hello LSM) has been restored, it is potentially inconsistent with hello shard entry in hello GSM.</span></span> <span data-ttu-id="129e4-188">這個範例程式碼中，外部 hello 分區已還原，和重新命名 toohello 原始 hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="129e4-188">Outside of this example code, hello shard was restored and renamed toohello original name of hello database.</span></span> <span data-ttu-id="129e4-189">因為它已還原，則會假設在 hello LSM hello 對應為 hello 受信任的對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-189">Since it was restored, it is assumed hello mapping in hello LSM is hello trusted mapping.</span></span> 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a><span data-ttu-id="129e4-190">地理容錯移轉 （還原） 的 hello 分區之後更新分區位置</span><span class="sxs-lookup"><span data-stu-id="129e4-190">Updating shard locations after a geo-failover (restore) of hello shards</span></span>
<span data-ttu-id="129e4-191">如果沒有地理容錯移轉，hello 次要資料庫的寫入存取，而會變成 hello 新的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="129e4-191">If there is a geo-failover, hello secondary database is made write accessible and becomes hello new primary database.</span></span> <span data-ttu-id="129e4-192">hello hello 伺服器和資料庫的名稱可能 hello （取決於您的組態），可能不同於 hello 原始的主要複本。</span><span class="sxs-lookup"><span data-stu-id="129e4-192">hello name of hello server, and potentially hello database (depending on your configuration), may be different from hello original primary.</span></span> <span data-ttu-id="129e4-193">因此 hello hello GSM 中的 hello 分區對應項目，必須修正 LSM。</span><span class="sxs-lookup"><span data-stu-id="129e4-193">Therefore hello mapping entries for hello shard in hello GSM and LSM must be fixed.</span></span> <span data-ttu-id="129e4-194">同樣地，如果 hello 資料庫是還原的 tooa 不同的名稱或位置或 tooan 早的時間點，這可能會導致不一致 hello 分區對應。</span><span class="sxs-lookup"><span data-stu-id="129e4-194">Similarly, if hello database is restored tooa different name or location, or tooan earlier point in time, this might cause inconsistencies in hello shard maps.</span></span> <span data-ttu-id="129e4-195">hello 分區對應管理員處理 hello 發佈的開啟連接 toohello 正確的資料庫。</span><span class="sxs-lookup"><span data-stu-id="129e4-195">hello Shard Map Manager handles hello distribution of open connections toohello correct database.</span></span> <span data-ttu-id="129e4-196">散發根據 hello 分區對應和 hello 的 hello hello 應用程式要求目標的 hello 分區化索引鍵的值中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="129e4-196">Distribution is based on hello data in hello shard map and hello value of hello sharding key that is hello target of hello applications request.</span></span> <span data-ttu-id="129e4-197">地理容錯移轉之後, 必須 hello 正確的伺服器名稱、 資料庫名稱與 hello 復原之資料庫的分區對應更新這項資訊。</span><span class="sxs-lookup"><span data-stu-id="129e4-197">After a geo-failover, this information must be updated with hello accurate server name, database name and shard mapping of hello recovered database.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="129e4-198">最佳作法</span><span class="sxs-lookup"><span data-stu-id="129e4-198">Best practices</span></span>
<span data-ttu-id="129e4-199">地理容錯移轉和復原是通常由雲端系統管理員刻意利用 Azure SQL Database 的業務續航力功能的其中一個 hello 應用程式管理的作業。</span><span class="sxs-lookup"><span data-stu-id="129e4-199">Geo-failover and recovery are operations typically managed by a cloud administrator of hello application intentionally utilizing one of Azure SQL Databases business continuity features.</span></span> <span data-ttu-id="129e4-200">營運持續計劃需要處理程序、 程序，以及業務營運能夠持續不中斷的量值 tooensure。</span><span class="sxs-lookup"><span data-stu-id="129e4-200">Business continuity planning requires processes, procedures, and measures tooensure that business operations can continue without interruption.</span></span> <span data-ttu-id="129e4-201">hello 方法應該使用 hello RecoveryManager 類別的一部分內這個工作流程 tooensure hello GSM 和 LSM 都保持最新依據採取 hello 復原動作。</span><span class="sxs-lookup"><span data-stu-id="129e4-201">hello methods available as part of hello RecoveryManager class should be used within this work flow tooensure hello GSM and LSM are kept up-to-date based on hello recovery action taken.</span></span> <span data-ttu-id="129e4-202">有五個基本步驟 tooproperly 確保 hello GSM 和 LSM 反映 hello 容錯移轉事件之後的正確資訊。</span><span class="sxs-lookup"><span data-stu-id="129e4-202">There are five basic steps tooproperly ensuring hello GSM and LSM reflect hello accurate information after a failover event.</span></span> <span data-ttu-id="129e4-203">hello 應用程式程式碼 tooexecute 這些步驟可以整合到現有的工具和工作流程。</span><span class="sxs-lookup"><span data-stu-id="129e4-203">hello application code tooexecute these steps can be integrated into existing tools and workflow.</span></span> 

1. <span data-ttu-id="129e4-204">擷取 hello ShardMapManager hello RecoveryManager。</span><span class="sxs-lookup"><span data-stu-id="129e4-204">Retrieve hello RecoveryManager from hello ShardMapManager.</span></span> 
2. <span data-ttu-id="129e4-205">卸離 hello hello 分區對應從舊的分區。</span><span class="sxs-lookup"><span data-stu-id="129e4-205">Detach hello old shard from hello shard map.</span></span>
3. <span data-ttu-id="129e4-206">附加 hello 新分區 toohello 分區對應，包括 hello 新分區的位置。</span><span class="sxs-lookup"><span data-stu-id="129e4-206">Attach hello new shard toohello shard map, including hello new shard location.</span></span>
4. <span data-ttu-id="129e4-207">Hello GSM 和 LSM hello 之間的對應中，偵測到不一致。</span><span class="sxs-lookup"><span data-stu-id="129e4-207">Detect inconsistencies in hello mapping between hello GSM and LSM.</span></span> 
5. <span data-ttu-id="129e4-208">解決 hello GSM 與 hello LSM，信任 hello LSM 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="129e4-208">Resolve differences between hello GSM and hello LSM, trusting hello LSM.</span></span> 

<span data-ttu-id="129e4-209">這個範例會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="129e4-209">This example performs hello following steps:</span></span>

1. <span data-ttu-id="129e4-210">移除 hello 反映分區位置 hello 容錯移轉事件之前的分區對應中的分區。</span><span class="sxs-lookup"><span data-stu-id="129e4-210">Removes shards from hello Shard Map that reflect shard locations before hello failover event.</span></span>
2. <span data-ttu-id="129e4-211">附加分區 toohello 分區對應反映 hello 新分區的位置 (hello 參數 」 Configuration.SecondaryServer"hello 新的伺服器名稱，但 hello 相同資料庫名稱)。</span><span class="sxs-lookup"><span data-stu-id="129e4-211">Attaches shards toohello Shard Map reflecting hello new shard locations (hello parameter "Configuration.SecondaryServer" is hello new server name but hello same database name).</span></span>
3. <span data-ttu-id="129e4-212">藉由偵測 hello GSM 與 hello LSM 為每個分區之間的對應差異擷取 hello 復原語彙基元。</span><span class="sxs-lookup"><span data-stu-id="129e4-212">Retrieves hello recovery tokens by detecting mapping differences between hello GSM and hello LSM for each shard.</span></span> 
4. <span data-ttu-id="129e4-213">解析從 hello LSM 的每個分區的信任 hello 對應 hello 不一致。</span><span class="sxs-lookup"><span data-stu-id="129e4-213">Resolves hello inconsistencies by trusting hello mapping from hello LSM of each shard.</span></span> 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

