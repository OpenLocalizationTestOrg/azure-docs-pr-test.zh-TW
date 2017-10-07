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
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>使用 hello RecoveryManager 類別 toofix 分區對應問題
hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx)類別提供 hello 能力 tooeasily 偵測並修正任何不一致性 hello 全域分區對應 (GSM) 與分區化資料庫環境中的 hello 本機分區對應 (LSM) 之間的 ADO.Net 應用程式。 

hello GSM 和 LSM 追蹤 hello 對應之每個資料庫分區化的環境中。 有時候，hello GSM 與 hello LSM 之間發生中斷。 在此情況下，使用 hello RecoveryManager 類別 toodetect 並修復 hello 中斷。

hello RecoveryManager 類別屬於 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)。 

![分區對應][1]

關於詞彙定義，請參閱 [彈性資料庫工具字彙](sql-database-elastic-scale-glossary.md)。 如何 hello toounderstand **ShardMapManager**使用的 toomanage 資料在分區化解決方案中，請參閱[分區對應管理](sql-database-elastic-scale-shard-map-management.md)。

## <a name="why-use-hello-recovery-manager"></a>為何要使用 hello 復原管理員？
在分區化資料庫環境中，每個資料庫有一個租用戶，而每個伺服器中有許多資料庫。 可以也有許多伺服器 hello 環境中。 每個資料庫會在 hello 分區對應中，對應，以便呼叫能夠路由的 toohello 正確的伺服器和資料庫。 資料庫會追蹤根據 tooa**分區化索引鍵**，並指派每個分區**鍵值範圍**。 例如，分區化索引鍵可能代表 hello 客戶名稱從"D"太"F.的" hello 所有分區 （也稱為資料庫） 的對應，而且其對應的範圍會包含在 hello**全域分區對應 (GSM)**。 每個資料庫也包含的 hello 範圍包含在 hello 就所謂的 hello 分區對應**本機分區對應 (LSM)**。 當應用程式連接 tooa 分區時，快速擷取 hello 應用程式快取 hello 對應。 hello LSM 是使用的 toovalidate 快取資料。 

hello GSM 和 LSM 變得不同步的 hello 下列原因：

1. 分區，其範圍相信 toono 較長的 hello 刪除作業會使用或重新命名的分區中。 刪除分區會導致 **被遺棄的分區對應**。 同樣地，重新命名的資料庫可能造成被遺棄的分區對應。 根據 hello 的 hello 變更的意圖，hello 分區可能需要移除 toobe 或 hello 分區位置需要 toobe 更新。 toorecover 已刪除的資料庫，請參閱[還原已刪除的資料庫](sql-database-recovery-using-backups.md)。
2. 發生異地備援容錯移轉事件。 toocontinue，一個必須更新 hello 伺服器名稱及分區對應中的所有分區分區對應管理員 hello 應用程式，然後更新 hello 分區對應詳細資料的資料庫名稱。 地理容錯移轉時，應該自動化這類復原邏輯 hello 容錯移轉工作流程內。 自動化修復動作可為異地備援的資料庫啟用順暢的管理能力，並避免人工的動作。 關於資料庫是否有資料中心中斷，請參閱選項 toorecover toolearn[業務續航力](sql-database-business-continuity.md)和[嚴重損壞修復](sql-database-disaster-recovery.md)。
3. 分區或 hello ShardMapManager 資料庫會還原的 tooan 稍早的點的時間。 toolearn 相關時間點復原使用備份，請參閱[使用備份復原](sql-database-recovery-using-backups.md)。

如需有關 Azure SQL Database 彈性資料庫工具、 地理複寫和還原的詳細資訊，請參閱 hello 下列： 

* [概觀：雲端商務持續性和 SQL Database 的資料庫災害復原](sql-database-business-continuity.md) 
* [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)  
* [ShardMap 管理](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>從 ShardMapManager 擷取 RecoveryManager
hello 第一個步驟是 toocreate RecoveryManager 執行個體。 hello [GetRecoveryManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx)傳回 hello hello 目前復原管理員[ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)執行個體。 將對應 tooaddress hello 分區中的不一致，您必須先擷取 hello RecoveryManager hello 特定分區對應。 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

在此範例中，會從 hello ShardMapManager hello RecoveryManager 組初始化。 hello ShardMapManager 包含 ShardMap 也已經初始化。 

因為此應用程式程式碼操作 hello 分區對應本身，hello hello factory 方法中使用的認證 (在上述範例中，hello smmConnectionString) 應該是具有 hello 所參考的 hello GSM 資料庫讀寫權限的認證連接字串。 這些認證所用認證 tooopen 連線資料依存路由通常不同。 如需詳細資訊，請參閱[hello 彈性資料庫用戶端中使用認證](sql-database-elastic-scale-manage-credentials.md)。

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>從 hello ShardMap 移除分區之後會刪除分區
hello [DetachShard 方法](https://msdn.microsoft.com/library/azure/dn842083.aspx)卸離 hello 根據分區指定 hello 分區對應，並刪除 hello 分區相關聯的對應。  

* hello 分區位置，特別是伺服器名稱和資料庫名稱，要卸離的 hello 分區 hello 位置參數。 
* hello shardMapName 參數是 hello 分區對應名稱。 這只是需要： 當多個分區對應由 hello 相同分區對應管理員。 選用。 


> [!IMPORTANT]
> 只有在特定 hello 更新對應的 hello 範圍是空的請使用這項技術。 上述的 hello 方法不會檢查正在移動的 hello 範圍的資料，因此最適合 tooinclude 會檢查您的程式碼中。
>

這個範例會移除 hello 分區對應中的分區。 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

hello 分區對應會反映在 hello GSM hello 分區的 hello 刪除之前的 hello 分區位置。 因為已刪除 hello 分區，它會假設這是有意的且 hello 分區化索引鍵範圍不再使用中。 如果情況並非如此，您可以執行時間點還原， toorecover hello 分區從較早的時間點。 （在此情況下，檢閱下列區段 toodetect 分區不一致的 hello）。toorecover，請參閱[時間點復原](sql-database-recovery-using-backups.md)。

因為它假設 hello 資料庫刪除有意，hello 最終的系統管理清理動作是 toodelete hello 項目 toohello 分區 hello 分區對應管理員中。 這可避免不慎撰寫未預期的資訊 tooa 範圍 hello 應用程式。

## <a name="toodetect-mapping-differences"></a>toodetect 對應的差異
hello [DetectMappingDifferences 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx)選取並傳回 hello 分區對應 （本機或全域） 的其中一個為 hello 事實來源調解 （GSM 和 LSM） 這兩個分區對應上的對應。

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* hello*位置*指定 hello 伺服器名稱和資料庫名稱。 
* hello *shardMapName*參數是 hello 分區對應名稱。 這只是需要多個分區對應的 hello 都受相同的分區對應管理員。 選用。 

## <a name="tooresolve-mapping-differences"></a>tooresolve 對應的差異
hello [ResolveMappingDifferences 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx)為 hello 事實來源中選取一個 hello 分區對應 （本機或全域） 並調解 （GSM 和 LSM） 這兩個分區對應上的對應。

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* hello *RecoveryToken*參數列舉 hello 對應 hello GSM 之間 hello LSM hello 特定分區的 hello 差異。 
* hello [MappingDifferenceResolution 列舉](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx)是使用的 tooindicate hello 方法來解析 hello hello 分區對應的差異。 
* **MappingDifferenceResolution.KeepShardMapping**時，建議的 hello LSM 包含 hello 精確對應，因此應該使用 hello 分區中的 hello 對應。 這是通常 hello 情況下，如果容錯移轉： hello 分區現在位於新的伺服器上。 因為從 hello GSM （使用 hello RecoveryManager.DetachShard 方法） 時，您必須先移除 hello 分區，其對應不再存在 hello GSM 上。 因此，hello LSM 必須使用的 toore-建立 hello 分區對應。

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>附加分區 toohello ShardMap 分區還原之後
hello [AttachShard 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx)附加 hello 給定的分區 toohello 分區對應。 然後會偵測任何分區對應不一致，並更新 hello 對應 toomatch hello 分區 hello hello 分區還原點。 它會假設該 hello 資料庫也是重新命名的 tooreflect hello 原始資料庫名稱 （之前已還原 hello 分區），因為 hello 時間點還原預設值 tooa hello 時間戳記附加新的資料庫。 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* hello*位置*參數是 hello 伺服器名稱和資料庫名稱，要附加的 hello 分區。 
* hello *shardMapName*參數是 hello 分區對應名稱。 這只是需要： 當多個分區對應由 hello 相同分區對應管理員。 選用。 

這個範例會將已經從較早的中點時間最近還原分區 toohello 分區對應。 Hello 分區 (也就是在 hello LSM hello 分區對應的 hello) 已還原，因為它是與 hello GSM 中的 hello 分區項目可能不一致。 這個範例程式碼中，外部 hello 分區已還原，和重新命名 toohello 原始 hello 資料庫名稱。 因為它已還原，則會假設在 hello LSM hello 對應為 hello 受信任的對應。 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>地理容錯移轉 （還原） 的 hello 分區之後更新分區位置
如果沒有地理容錯移轉，hello 次要資料庫的寫入存取，而會變成 hello 新的主要資料庫。 hello hello 伺服器和資料庫的名稱可能 hello （取決於您的組態），可能不同於 hello 原始的主要複本。 因此 hello hello GSM 中的 hello 分區對應項目，必須修正 LSM。 同樣地，如果 hello 資料庫是還原的 tooa 不同的名稱或位置或 tooan 早的時間點，這可能會導致不一致 hello 分區對應。 hello 分區對應管理員處理 hello 發佈的開啟連接 toohello 正確的資料庫。 散發根據 hello 分區對應和 hello 的 hello hello 應用程式要求目標的 hello 分區化索引鍵的值中的 hello 資料。 地理容錯移轉之後, 必須 hello 正確的伺服器名稱、 資料庫名稱與 hello 復原之資料庫的分區對應更新這項資訊。 

## <a name="best-practices"></a>最佳作法
地理容錯移轉和復原是通常由雲端系統管理員刻意利用 Azure SQL Database 的業務續航力功能的其中一個 hello 應用程式管理的作業。 營運持續計劃需要處理程序、 程序，以及業務營運能夠持續不中斷的量值 tooensure。 hello 方法應該使用 hello RecoveryManager 類別的一部分內這個工作流程 tooensure hello GSM 和 LSM 都保持最新依據採取 hello 復原動作。 有五個基本步驟 tooproperly 確保 hello GSM 和 LSM 反映 hello 容錯移轉事件之後的正確資訊。 hello 應用程式程式碼 tooexecute 這些步驟可以整合到現有的工具和工作流程。 

1. 擷取 hello ShardMapManager hello RecoveryManager。 
2. 卸離 hello hello 分區對應從舊的分區。
3. 附加 hello 新分區 toohello 分區對應，包括 hello 新分區的位置。
4. Hello GSM 和 LSM hello 之間的對應中，偵測到不一致。 
5. 解決 hello GSM 與 hello LSM，信任 hello LSM 之間的差異。 

這個範例會執行下列步驟的 hello:

1. 移除 hello 反映分區位置 hello 容錯移轉事件之前的分區對應中的分區。
2. 附加分區 toohello 分區對應反映 hello 新分區的位置 (hello 參數 」 Configuration.SecondaryServer"hello 新的伺服器名稱，但 hello 相同資料庫名稱)。
3. 藉由偵測 hello GSM 與 hello LSM 為每個分區之間的對應差異擷取 hello 復原語彙基元。 
4. 解析從 hello LSM 的每個分區的信任 hello 對應 hello 不一致。 
   
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

