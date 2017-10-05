---
title: "使用復原管理員修正分區對應問題 | Microsoft Docs"
description: "使用 RecoveryManager 類別來解決分區對應的問題"
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
ms.openlocfilehash: e60e2295484873ea15d52108b7d619319a57827f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-recoverymanager-class-to-fix-shard-map-problems"></a><span data-ttu-id="ca696-103">使用 RecoveryManager 類別來修正分區對應問題</span><span class="sxs-lookup"><span data-stu-id="ca696-103">Using the RecoveryManager class to fix shard map problems</span></span>
<span data-ttu-id="ca696-104">[RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) 類別提供 ADO.Net 應用程式輕鬆偵測，並修正分區化資料庫環境中全域分區對應 (GSM) 和本機分區對應 (LSM) 中任何不一致的能力。</span><span class="sxs-lookup"><span data-stu-id="ca696-104">The [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) class provides ADO.Net applications the ability to easily detect and correct any inconsistencies between the global shard map (GSM) and the local shard map (LSM) in a sharded database environment.</span></span> 

<span data-ttu-id="ca696-105">GSM 和 LSM 會追蹤分區化環境中每個資料庫的對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-105">The GSM and LSM track the mapping of each database in a sharded environment.</span></span> <span data-ttu-id="ca696-106">但偶爾 GSM 和 LSM 之間會發生中斷的情況。</span><span class="sxs-lookup"><span data-stu-id="ca696-106">Occasionally, a break occurs between the GSM and the LSM.</span></span> <span data-ttu-id="ca696-107">此時，請使用 RecoveryManager 類別來偵測並修復中斷的問題。</span><span class="sxs-lookup"><span data-stu-id="ca696-107">In that case, use the RecoveryManager class to detect and repair the break.</span></span>

<span data-ttu-id="ca696-108">RecoveryManager 類別是 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="ca696-108">The RecoveryManager class is part of the [Elastic Database client library](sql-database-elastic-database-client-library.md).</span></span> 

![分區對應][1]

<span data-ttu-id="ca696-110">關於詞彙定義，請參閱 [彈性資料庫工具字彙](sql-database-elastic-scale-glossary.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-110">For term definitions, see [Elastic Database tools glossary](sql-database-elastic-scale-glossary.md).</span></span> <span data-ttu-id="ca696-111">若要了解 **ShardMapManager** 如何用來管理分區化解決方案中的資料，請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-111">To understand how the **ShardMapManager** is used to manage data in a sharded solution, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span>

## <a name="why-use-the-recovery-manager"></a><span data-ttu-id="ca696-112">為何使用復原管理員？</span><span class="sxs-lookup"><span data-stu-id="ca696-112">Why use the recovery manager?</span></span>
<span data-ttu-id="ca696-113">在分區化資料庫環境中，每個資料庫有一個租用戶，而每個伺服器中有許多資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca696-113">In a sharded database environment, there is one tenant per database, and many databases per server.</span></span> <span data-ttu-id="ca696-114">環境中也可能會有許多伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca696-114">There can also be many servers in the environment.</span></span> <span data-ttu-id="ca696-115">每個資料庫都會在分區對應中對應，以便呼叫可以路由至正確的伺服器和資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca696-115">Each database is mapped in the shard map, so calls can be routed to the correct server and database.</span></span> <span data-ttu-id="ca696-116">根據**分區化索引鍵**追蹤資料庫，而每個分區會被指派**某個範圍的索引鍵值**。</span><span class="sxs-lookup"><span data-stu-id="ca696-116">Databases are tracked according to a **sharding key**, and each shard is assigned a **range of key values**.</span></span> <span data-ttu-id="ca696-117">例如，分區化索引鍵可能代表客戶名稱從 "D" 到 "F"。</span><span class="sxs-lookup"><span data-stu-id="ca696-117">For example, a sharding key may represent the customer names from "D" to "F."</span></span> <span data-ttu-id="ca696-118">所有分區 (也稱為資料庫) 和其對應範圍的對應都包含在 **全域分區對應 (GSM)**中。</span><span class="sxs-lookup"><span data-stu-id="ca696-118">The mapping of all shards (aka databases) and their mapping ranges are contained in the **global shard map (GSM)**.</span></span> <span data-ttu-id="ca696-119">每個資料庫也包含分區上所包含之範圍的對應 (稱為**本機分區對應 (LSM)**)。</span><span class="sxs-lookup"><span data-stu-id="ca696-119">Each database also contains a map of the ranges contained on the shard that is known as the **local shard map (LSM)**.</span></span> <span data-ttu-id="ca696-120">當應用程式連接到分區時，會隨著應用程式快取對應以供快速擷取。</span><span class="sxs-lookup"><span data-stu-id="ca696-120">When an app connects to a shard, the mapping is cached with the app for quick retrieval.</span></span> <span data-ttu-id="ca696-121">LSM 用來驗證快取的資料。</span><span class="sxs-lookup"><span data-stu-id="ca696-121">The LSM is used to validate cached data.</span></span> 

<span data-ttu-id="ca696-122">GSM 和 LSM 可能因為以下原因變成不同步：</span><span class="sxs-lookup"><span data-stu-id="ca696-122">The GSM and LSM may become out of sync for the following reasons:</span></span>

1. <span data-ttu-id="ca696-123">刪除其範圍被認為不再使用中的分區，或重新命名分區。</span><span class="sxs-lookup"><span data-stu-id="ca696-123">The deletion of a shard whose range is believed to no longer be in use, or renaming of a shard.</span></span> <span data-ttu-id="ca696-124">刪除分區會導致 **被遺棄的分區對應**。</span><span class="sxs-lookup"><span data-stu-id="ca696-124">Deleting a shard results in an **orphaned shard mapping**.</span></span> <span data-ttu-id="ca696-125">同樣地，重新命名的資料庫可能造成被遺棄的分區對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-125">Similarly, a renamed database can cause an orphaned shard mapping.</span></span> <span data-ttu-id="ca696-126">根據變更的目的而定，可能需要移除分區或更新分區位置。</span><span class="sxs-lookup"><span data-stu-id="ca696-126">Depending on the intent of the change, the shard may need to be removed or the shard location needs to be updated.</span></span> <span data-ttu-id="ca696-127">若要復原已刪除的資料庫，請參閱[還原已刪除的資料庫](sql-database-recovery-using-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-127">To recover a deleted database, see [Restore a deleted database](sql-database-recovery-using-backups.md).</span></span>
2. <span data-ttu-id="ca696-128">發生異地備援容錯移轉事件。</span><span class="sxs-lookup"><span data-stu-id="ca696-128">A geo-failover event occurs.</span></span> <span data-ttu-id="ca696-129">若要繼續，必須更新伺服器名稱及應用程式中分區對應管理員的資料庫名稱，然後更新分區對應中所有分區的分區對應詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ca696-129">To continue, one must update the server name, and database name of shard map manager in the application and then update the shard mapping details for all shards in a shard map.</span></span> <span data-ttu-id="ca696-130">如果有異地容錯移轉，這類復原邏輯應該在容錯移轉工作流程內自動執行。</span><span class="sxs-lookup"><span data-stu-id="ca696-130">If there is a geo-failover, such recovery logic should be automated within the failover workflow.</span></span> <span data-ttu-id="ca696-131">自動化修復動作可為異地備援的資料庫啟用順暢的管理能力，並避免人工的動作。</span><span class="sxs-lookup"><span data-stu-id="ca696-131">Automating recovery actions enables a frictionless manageability for geo-enabled databases and avoids manual human actions.</span></span> <span data-ttu-id="ca696-132">若要了解在資料中心中斷時復原資料庫的選項，請參閱[商務持續性](sql-database-business-continuity.md)和[災害復原](sql-database-disaster-recovery.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-132">To learn about options to recover a database if there is a data center outage, see [Business Continuity](sql-database-business-continuity.md) and [Disaster Recovery](sql-database-disaster-recovery.md).</span></span>
3. <span data-ttu-id="ca696-133">分區或 ShardMapManager 資料庫會還原到較早的時間點。</span><span class="sxs-lookup"><span data-stu-id="ca696-133">Either a shard or the ShardMapManager database is restored to an earlier point-in time.</span></span> <span data-ttu-id="ca696-134">若要了解如何使用備份進行時間點復原，請參閱[使用備份進行復原](sql-database-recovery-using-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-134">To learn about point in time recovery using backups, see [Recovery using backups](sql-database-recovery-using-backups.md).</span></span>

<span data-ttu-id="ca696-135">如需有關 Azure SQL Database 彈性資料庫工具、異地複寫及還原的詳細資訊，請參閱下列連結：</span><span class="sxs-lookup"><span data-stu-id="ca696-135">For more information about Azure SQL Database Elastic Database tools, geo-replication and Restore, see the following:</span></span> 

* [<span data-ttu-id="ca696-136">概觀：雲端商務持續性和 SQL Database 的資料庫災害復原</span><span class="sxs-lookup"><span data-stu-id="ca696-136">Overview: Cloud business continuity and database disaster recovery with SQL Database</span></span>](sql-database-business-continuity.md) 
* [<span data-ttu-id="ca696-137">開始使用彈性資料庫工具</span><span class="sxs-lookup"><span data-stu-id="ca696-137">Get started with elastic database tools</span></span>](sql-database-elastic-scale-get-started.md)  
* [<span data-ttu-id="ca696-138">ShardMap 管理</span><span class="sxs-lookup"><span data-stu-id="ca696-138">ShardMap Management</span></span>](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a><span data-ttu-id="ca696-139">從 ShardMapManager 擷取 RecoveryManager</span><span class="sxs-lookup"><span data-stu-id="ca696-139">Retrieving RecoveryManager from a ShardMapManager</span></span>
<span data-ttu-id="ca696-140">第一個步驟是建立 RecoveryManager 執行個體。</span><span class="sxs-lookup"><span data-stu-id="ca696-140">The first step is to create a RecoveryManager instance.</span></span> <span data-ttu-id="ca696-141">[GetRecoveryManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx)會傳回目前的 [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) 執行個體的復原管理員。</span><span class="sxs-lookup"><span data-stu-id="ca696-141">The [GetRecoveryManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) returns the recovery manager for the current [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) instance.</span></span> <span data-ttu-id="ca696-142">若要解決分區對應中的任何不一致，您必須先擷取特定分區對應的 RecoveryManager。</span><span class="sxs-lookup"><span data-stu-id="ca696-142">To address any inconsistencies in the shard map, you must first retrieve the RecoveryManager for the particular shard map.</span></span> 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

<span data-ttu-id="ca696-143">在此範例中，RecoveryManager 是從 ShardMapManager 初始化。</span><span class="sxs-lookup"><span data-stu-id="ca696-143">In this example, the RecoveryManager is initialized from the ShardMapManager.</span></span> <span data-ttu-id="ca696-144">ShardMapManager 包含也已經初始化的 ShardMap。</span><span class="sxs-lookup"><span data-stu-id="ca696-144">The ShardMapManager containing a ShardMap is also already initialized.</span></span> 

<span data-ttu-id="ca696-145">由於此應用程式程式碼會操作分區對應本身，因此在 Factory 方法中使用的認證 (在上述範例中為 smmConnectionString) 應該是在連接字串所參考的 GSM 資料庫上具備讀寫權限的認證。</span><span class="sxs-lookup"><span data-stu-id="ca696-145">Since this application code manipulates the shard map itself, the credentials used in the factory method (in the preceding example, smmConnectionString) should be credentials that have read-write permissions on the GSM database referenced by the connection string.</span></span> <span data-ttu-id="ca696-146">這些認證通常不同於用來對資料獨立路由開啟連接的認證。</span><span class="sxs-lookup"><span data-stu-id="ca696-146">These credentials are typically different from credentials used to open connections for data-dependent routing.</span></span> <span data-ttu-id="ca696-147">如需詳細資訊，請參閱 [在彈性資料庫用戶端中使用認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-147">For more information, see [Using credentials in the elastic database client](sql-database-elastic-scale-manage-credentials.md).</span></span>

## <a name="removing-a-shard-from-the-shardmap-after-a-shard-is-deleted"></a><span data-ttu-id="ca696-148">刪除分區之後從 ShardMap 移除分區</span><span class="sxs-lookup"><span data-stu-id="ca696-148">Removing a shard from the ShardMap after a shard is deleted</span></span>
<span data-ttu-id="ca696-149">[DetachShard 方法](https://msdn.microsoft.com/library/azure/dn842083.aspx) 會從給定的分區卸離分區對應，並刪除與分區相關聯的對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-149">The [DetachShard method](https://msdn.microsoft.com/library/azure/dn842083.aspx) detaches the given shard from the shard map and deletes mappings associated with the shard.</span></span>  

* <span data-ttu-id="ca696-150">location 參數是分區位置，特別是要卸離的分區的伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-150">The location parameter is the shard location, specifically server name and database name, of the shard being detached.</span></span> 
* <span data-ttu-id="ca696-151">shardMapName 參數是分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-151">The shardMapName parameter is the shard map name.</span></span> <span data-ttu-id="ca696-152">只有在多個分區對應是由相同的分區對應管理員管理時才為必要。</span><span class="sxs-lookup"><span data-stu-id="ca696-152">This is only required when multiple shard maps are managed by the same shard map manager.</span></span> <span data-ttu-id="ca696-153">選用。</span><span class="sxs-lookup"><span data-stu-id="ca696-153">Optional.</span></span> 


> [!IMPORTANT]
> <span data-ttu-id="ca696-154">只有在您確定更新對應的範圍是空白時，才可使用這項技術。</span><span class="sxs-lookup"><span data-stu-id="ca696-154">Use this technique only if you are certain that the range for the updated mapping is empty.</span></span> <span data-ttu-id="ca696-155">上述方法並不會檢查要移動的資料範圍，因此您最好在程式碼中納入檢查。</span><span class="sxs-lookup"><span data-stu-id="ca696-155">The methods above do not check data for the range being moved, so it is best to include checks in your code.</span></span>
>

<span data-ttu-id="ca696-156">這個範例會從分區對應中移除分區。</span><span class="sxs-lookup"><span data-stu-id="ca696-156">This example removes shards from the shard map.</span></span> 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

<span data-ttu-id="ca696-157">此分區對應會反映刪除分區之前，分區在 GSM 中的位置。</span><span class="sxs-lookup"><span data-stu-id="ca696-157">The shard map reflects the shard location in the GSM before the deletion of the shard.</span></span> <span data-ttu-id="ca696-158">因為已刪除分區，會假設這是特意的，而且分區化索引鍵範圍已不再使用中。</span><span class="sxs-lookup"><span data-stu-id="ca696-158">Because the shard was deleted, it is assumed this was intentional, and the sharding key range is no longer in use.</span></span> <span data-ttu-id="ca696-159">如果情況並非如此，您可以執行時間點還原，</span><span class="sxs-lookup"><span data-stu-id="ca696-159">If not, you can execute point-in time restore.</span></span> <span data-ttu-id="ca696-160">從較早的時間點復原分區。</span><span class="sxs-lookup"><span data-stu-id="ca696-160">to recover the shard from an earlier point-in-time.</span></span> <span data-ttu-id="ca696-161">(在該情況下，請檢閱下一節來偵測分區不一致的情形。)若要復原，請參閱[時間點復原](sql-database-recovery-using-backups.md)。</span><span class="sxs-lookup"><span data-stu-id="ca696-161">(In that case, review the following section to detect shard inconsistencies.) To recover, see [Point in time recovery](sql-database-recovery-using-backups.md).</span></span>

<span data-ttu-id="ca696-162">由於假設刪除資料庫是在預期中，最終的系統管理清除動作是刪除分區對應管理員中分區的項目。</span><span class="sxs-lookup"><span data-stu-id="ca696-162">Since it is assumed the database deletion was intentional, the final administrative cleanup action is to delete the entry to the shard in the shard map manager.</span></span> <span data-ttu-id="ca696-163">這可避免應用程式不小心將資訊寫入至未預期的範圍。</span><span class="sxs-lookup"><span data-stu-id="ca696-163">This prevents the application from inadvertently writing information to a range that is not expected.</span></span>

## <a name="to-detect-mapping-differences"></a><span data-ttu-id="ca696-164">偵測對應的差異</span><span class="sxs-lookup"><span data-stu-id="ca696-164">To detect mapping differences</span></span>
<span data-ttu-id="ca696-165">[DetectMappingDifferences 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) 可選取並傳回其中一個分區對應 (本機或全域) 做為真實來源，並調解兩個分區對應 (GSM 和 LSM) 上的對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-165">The [DetectMappingDifferences method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) selects and returns one of the shard maps (either local or global) as the source of truth and reconciles mappings on both shard maps (GSM and LSM).</span></span>

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* <span data-ttu-id="ca696-166">*location* 指定伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-166">The *location* specifies the server name and database name.</span></span> 
* <span data-ttu-id="ca696-167">*shardMapName* 參數是分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-167">The *shardMapName* parameter is the shard map name.</span></span> <span data-ttu-id="ca696-168">只有在多個分區對應是由相同的分區對應管理員管理時才為必要。</span><span class="sxs-lookup"><span data-stu-id="ca696-168">This is only required if multiple shard maps are managed by the same shard map manager.</span></span> <span data-ttu-id="ca696-169">選用。</span><span class="sxs-lookup"><span data-stu-id="ca696-169">Optional.</span></span> 

## <a name="to-resolve-mapping-differences"></a><span data-ttu-id="ca696-170">解決對應的差異</span><span class="sxs-lookup"><span data-stu-id="ca696-170">To resolve mapping differences</span></span>
<span data-ttu-id="ca696-171">[ResolveMappingDifferences 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) 可選取其中一個分區對應 (本機或全域) 做為真實來源，並調解兩個分區對應 (GSM 和 LSM) 上的對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-171">The [ResolveMappingDifferences method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) selects one of the shard maps (either local or global) as the source of truth and reconciles mappings on both shard maps (GSM and LSM).</span></span>

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* <span data-ttu-id="ca696-172">*RecoveryToken* 參數會列舉特定分區的 GSM 與 LSM 之間對應的差異。</span><span class="sxs-lookup"><span data-stu-id="ca696-172">The *RecoveryToken* parameter enumerates the differences in the mappings between the GSM and the LSM for the specific shard.</span></span> 
* <span data-ttu-id="ca696-173">[MappingDifferenceResolution 列舉](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) 用來指出用於解析分區對應之間差異的方法。</span><span class="sxs-lookup"><span data-stu-id="ca696-173">The [MappingDifferenceResolution enumeration](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) is used to indicate the method for resolving the difference between the shard mappings.</span></span> 
* <span data-ttu-id="ca696-174">當 LSM 包含正確的對應因而應該使用分區中的對應時，建議使用 **MappingDifferenceResolution.KeepShardMapping**。</span><span class="sxs-lookup"><span data-stu-id="ca696-174">**MappingDifferenceResolution.KeepShardMapping** is recommended that when the LSM contains the accurate mapping and therefore the mapping in the shard should be used.</span></span> <span data-ttu-id="ca696-175">當發生容錯移轉時，通常會是這種情況：分區現在位於新的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="ca696-175">This is typically the case if there is a failover: the shard now resides on a new server.</span></span> <span data-ttu-id="ca696-176">由於必須先從 GSM 中移除分區 (使用 RecoveryManager.DetachShard 方法)，GSM 上不再存在對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-176">Since the shard must first be removed from the GSM (using the RecoveryManager.DetachShard method), a mapping no longer exists on the GSM.</span></span> <span data-ttu-id="ca696-177">因此，必須使用 LSM 來重新建立分區對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-177">Therefore, the LSM must be used to re-establish the shard mapping.</span></span>

## <a name="attach-a-shard-to-the-shardmap-after-a-shard-is-restored"></a><span data-ttu-id="ca696-178">在還原分區之後將分區附加至 ShardMap</span><span class="sxs-lookup"><span data-stu-id="ca696-178">Attach a shard to the ShardMap after a shard is restored</span></span>
<span data-ttu-id="ca696-179">[AttachShard 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) 會將給定的分區附加至分區對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-179">The [AttachShard method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) attaches the given shard to the shard map.</span></span> <span data-ttu-id="ca696-180">然後它會偵測任何分區對應不一致，並更新對應以符合分區還原時間點的分區。</span><span class="sxs-lookup"><span data-stu-id="ca696-180">It then detects any shard map inconsistencies and updates the mappings to match the shard at the point of the shard restoration.</span></span> <span data-ttu-id="ca696-181">系統會假設資料庫也重新命名來反映原始資料庫名稱 (還原分區之前)，因為時間點還原預設是採用新資料庫再加上時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ca696-181">It is assumed that the database is also renamed to reflect the original database name (before the shard was restored), since the point-in time restoration defaults to a new database appended with the timestamp.</span></span> 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* <span data-ttu-id="ca696-182">*location* 參數是要附加的分區的伺服器名稱和資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-182">The *location* parameter is the server name and database name, of the shard being attached.</span></span> 
* <span data-ttu-id="ca696-183">*shardMapName* 參數是分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-183">The *shardMapName* parameter is the shard map name.</span></span> <span data-ttu-id="ca696-184">只有在多個分區對應是由相同的分區對應管理員管理時才為必要。</span><span class="sxs-lookup"><span data-stu-id="ca696-184">This is only required when multiple shard maps are managed by the same shard map manager.</span></span> <span data-ttu-id="ca696-185">選用。</span><span class="sxs-lookup"><span data-stu-id="ca696-185">Optional.</span></span> 

<span data-ttu-id="ca696-186">此範例會將分區新增到最近從較早時間點還原的分區對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-186">This example adds a shard to the shard map that has been recently restored from an earlier point-in time.</span></span> <span data-ttu-id="ca696-187">因為已還原分區 (也就是 LSM 中的分區對應)，該分區可能會與 GSM 中的分區項目不一致。</span><span class="sxs-lookup"><span data-stu-id="ca696-187">Since the shard (namely the mapping for the shard in the LSM) has been restored, it is potentially inconsistent with the shard entry in the GSM.</span></span> <span data-ttu-id="ca696-188">在這個範例程式碼之外，分區已還原並重新命名為資料庫的原始名稱。</span><span class="sxs-lookup"><span data-stu-id="ca696-188">Outside of this example code, the shard was restored and renamed to the original name of the database.</span></span> <span data-ttu-id="ca696-189">因為它已還原，就會假設 LSM 中的對應為受信任的對應。</span><span class="sxs-lookup"><span data-stu-id="ca696-189">Since it was restored, it is assumed the mapping in the LSM is the trusted mapping.</span></span> 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-the-shards"></a><span data-ttu-id="ca696-190">在分區的異地複寫容錯移轉 (還原) 之後更新分區位置</span><span class="sxs-lookup"><span data-stu-id="ca696-190">Updating shard locations after a geo-failover (restore) of the shards</span></span>
<span data-ttu-id="ca696-191">如果發生異地容錯移轉，次要資料庫會變成可供寫入存取，並成為新的主要資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca696-191">If there is a geo-failover, the secondary database is made write accessible and becomes the new primary database.</span></span> <span data-ttu-id="ca696-192">伺服器的名稱和可能的資料庫 (根據您的設定而定)，可能會將原始主要複本的不同。</span><span class="sxs-lookup"><span data-stu-id="ca696-192">The name of the server, and potentially the database (depending on your configuration), may be different from the original primary.</span></span> <span data-ttu-id="ca696-193">因此，必須修正 GSM 和 LSM 分區的對應項目。</span><span class="sxs-lookup"><span data-stu-id="ca696-193">Therefore the mapping entries for the shard in the GSM and LSM must be fixed.</span></span> <span data-ttu-id="ca696-194">同樣地，如果資料庫還原至不同的名稱或位置，或到較早的時間點，這可能會在分區對應中造成不一致。</span><span class="sxs-lookup"><span data-stu-id="ca696-194">Similarly, if the database is restored to a different name or location, or to an earlier point in time, this might cause inconsistencies in the shard maps.</span></span> <span data-ttu-id="ca696-195">分區對應管理員會處理開啟連接到正確資料庫的散發。</span><span class="sxs-lookup"><span data-stu-id="ca696-195">The Shard Map Manager handles the distribution of open connections to the correct database.</span></span> <span data-ttu-id="ca696-196">分配時，會根據分區對應中的資料和作為應用程式要求目標之分區化金鑰的值，進行分配。</span><span class="sxs-lookup"><span data-stu-id="ca696-196">Distribution is based on the data in the shard map and the value of the sharding key that is the target of the applications request.</span></span> <span data-ttu-id="ca696-197">異地複寫容錯移轉之後，必須以正確的伺服器名稱、資料庫名稱和修復資料庫的分區對應更新這項資訊。</span><span class="sxs-lookup"><span data-stu-id="ca696-197">After a geo-failover, this information must be updated with the accurate server name, database name and shard mapping of the recovered database.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="ca696-198">最佳作法</span><span class="sxs-lookup"><span data-stu-id="ca696-198">Best practices</span></span>
<span data-ttu-id="ca696-199">異地容錯移轉和復原是一般由應用程式的雲端系統管理員管理的作業，刻意利用 Azure SQL Database 其中一個商務持續性功能。</span><span class="sxs-lookup"><span data-stu-id="ca696-199">Geo-failover and recovery are operations typically managed by a cloud administrator of the application intentionally utilizing one of Azure SQL Databases business continuity features.</span></span> <span data-ttu-id="ca696-200">商務持續性計劃需要處理程序、程序和措施以確保商務運作能持續而不會中斷。</span><span class="sxs-lookup"><span data-stu-id="ca696-200">Business continuity planning requires processes, procedures, and measures to ensure that business operations can continue without interruption.</span></span> <span data-ttu-id="ca696-201">應該在此工作流程中使用隨著 RecoveryManager 類別提供的方法，以確保根據採取的修復動作，GSM 和 LSM 都處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="ca696-201">The methods available as part of the RecoveryManager class should be used within this work flow to ensure the GSM and LSM are kept up-to-date based on the recovery action taken.</span></span> <span data-ttu-id="ca696-202">在 5 個基本步驟可正確確保 GSM 和 LSM 在容錯移轉事件之後反映正確的資訊。</span><span class="sxs-lookup"><span data-stu-id="ca696-202">There are five basic steps to properly ensuring the GSM and LSM reflect the accurate information after a failover event.</span></span> <span data-ttu-id="ca696-203">執行這些步驟的應用程式程式碼可以整合至現有的工具和工作流程。</span><span class="sxs-lookup"><span data-stu-id="ca696-203">The application code to execute these steps can be integrated into existing tools and workflow.</span></span> 

1. <span data-ttu-id="ca696-204">從 ShardMapManager 擷取 RecoveryManager。</span><span class="sxs-lookup"><span data-stu-id="ca696-204">Retrieve the RecoveryManager from the ShardMapManager.</span></span> 
2. <span data-ttu-id="ca696-205">從分區對應卸離舊分區。</span><span class="sxs-lookup"><span data-stu-id="ca696-205">Detach the old shard from the shard map.</span></span>
3. <span data-ttu-id="ca696-206">將新的分區附加至分區對應，包括新的分區位置。</span><span class="sxs-lookup"><span data-stu-id="ca696-206">Attach the new shard to the shard map, including the new shard location.</span></span>
4. <span data-ttu-id="ca696-207">在 GSM 和 LSM 之間的對應中偵測到不一致。</span><span class="sxs-lookup"><span data-stu-id="ca696-207">Detect inconsistencies in the mapping between the GSM and LSM.</span></span> 
5. <span data-ttu-id="ca696-208">解決 GSM 和 LSM 之間的差異，信任 LSM。</span><span class="sxs-lookup"><span data-stu-id="ca696-208">Resolve differences between the GSM and the LSM, trusting the LSM.</span></span> 

<span data-ttu-id="ca696-209">此範例會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ca696-209">This example performs the following steps:</span></span>

1. <span data-ttu-id="ca696-210">從「分區對應」中移除反映容錯移轉事件之前分區位置的分區。</span><span class="sxs-lookup"><span data-stu-id="ca696-210">Removes shards from the Shard Map that reflect shard locations before the failover event.</span></span>
2. <span data-ttu-id="ca696-211">將分區附加至分區對應會反映新分區位置 (參數 "Configuration.SecondaryServer" 是是新伺服器名稱，但是相同的資料庫名稱)。</span><span class="sxs-lookup"><span data-stu-id="ca696-211">Attaches shards to the Shard Map reflecting the new shard locations (the parameter "Configuration.SecondaryServer" is the new server name but the same database name).</span></span>
3. <span data-ttu-id="ca696-212">透過偵測每個分區的 GSM 與 LSM 之間的對應差異來擷取復原權杖。</span><span class="sxs-lookup"><span data-stu-id="ca696-212">Retrieves the recovery tokens by detecting mapping differences between the GSM and the LSM for each shard.</span></span> 
4. <span data-ttu-id="ca696-213">透過信任來自每個分區 LSM 的對應，即可解決不一致情形。</span><span class="sxs-lookup"><span data-stu-id="ca696-213">Resolves the inconsistencies by trusting the mapping from the LSM of each shard.</span></span> 
   
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

