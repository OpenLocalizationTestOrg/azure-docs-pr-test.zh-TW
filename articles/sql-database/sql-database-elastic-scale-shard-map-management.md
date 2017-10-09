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
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>擴充資料庫與 hello 分區對應管理員
tooeasily 向外延展資料庫的 SQL Azure 使用分區對應管理員。 hello 分區對應管理員是一個特殊的資料庫維護分區集中的所有分區 （資料庫） 的通用對應資訊。 hello 中繼資料可讓應用程式 tooconnect toohello 正確的資料庫為基礎的 hello hello 值**分區化索引鍵**。 此外，每個分區集中 hello 包含追蹤 hello 本機分區資料的對應 (稱為**shardlet**)。 

![分區對應管理](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

了解如何建構這些對應是不可或缺的 tooshard 對應管理。 這是使用 hello [ShardMapManager 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)，找到在 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)toomanage 分區對應。  

## <a name="shard-maps-and-shard-mappings"></a>分區對應和分區對應方式
對於每個分區，您必須選取分區對應 toocreate hello 型別。 hello 選擇取決於 hello 資料庫架構： 

1. 每個資料庫的單一租用戶  
2. 每個資料庫的多個租用戶 (兩種類型)︰
   1. 清單對應
   2. 範圍對應

針對單一租用戶模型，建立 **清單對應** 分區對應。 hello 單一租用戶模型會指派一個資料庫，每個租用戶。 這是適用於 SaaS 開發人員的有效模式，因為它會簡化管理。

![清單對應][1]

hello 多租用戶模型會指派數個租用戶 tooa 單一資料庫 （和分散多個資料庫的租用戶的群組）。 當您希望產生每個租用戶 toohave 小型資料需要使用此模型。 在此模型中，我們會將指派租用戶 tooa 資料庫使用的範圍**範圍對應**。 

![範圍對應][2]

您可以實作多租用戶資料庫模型，使用或*清單對應*tooassign 多個租用戶 tooa 單一資料庫。 例如，DB1 是租用戶識別碼 1 和 5，請使用的 toostore 的資訊，而 DB2 儲存 7 租用戶和租用戶 10 的資料。 

![單一資料庫上的多個租用戶][3] 

### <a name="supported-net-types-for-sharding-keys"></a>分區化索引鍵支援的 .Net 型別
彈性延展支援 hello 下列.Net Framework 類型為分區化索引鍵：

* integer
* long
* guid
* byte[]  
* datetime
* timespan
* datetimeoffset

### <a name="list-and-range-shard-maps"></a>清單和範圍分區對應
建構分區對應時可以選擇使用**個別分區化索引鍵值的清單**，或使用**分區化索引鍵值的範圍**。 

### <a name="list-shard-maps"></a>清單分區對應
**分區**包含**shardlet** ，shardlet tooshards hello 對應也維持分區對應。 A**清單分區對應**hello 個別索引鍵值，找出 hello shardlet 與 hello 資料庫做為分區之間的關聯。  **列出對應**會明確且不同的索引鍵的值可以是對應的 toohello 相同的資料庫。 例如，索引鍵為 1 對應 tooDatabase A 並 3 到 6 的索引鍵值參考資料庫 b。

| Key | 分區位置 |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>範圍分區對應
在**範圍分區對應**，由一組描述 hello 索引鍵範圍**[低值、 最高值）**其中 hello*低值*hello hello 範圍和 hello中的最小金鑰*高價值*是 hello 高於 hello 範圍的第一個值。 

例如，**[0, 100)** 包含所有大於或等於 0 且小於 100 的整數。 請注意，支援多個範圍可以點 toohello 相同資料庫，以及脫離的範圍 (例如，[100200) 和 [400,600) 這兩個點 tooDatabase C hello 下面範例中。)

| Key | 分區位置 |
| --- | --- |
| [1,50) |Database_A |
| [50,100) |Database_B |
| [100,200) |Database_C |
| [400,600) |Database_C |
| ... |... |

如上所示的 hello 資料表的每一個都是一個概念的範例**ShardMap**物件。 每個資料列是個人的簡化的範例**PointMapping** （適用於 hello 清單分區對應） 或**RangeMapping** （適用於 hello 範圍分區對應） 物件。

## <a name="shard-map-manager"></a>分區對應管理員
Hello 用戶端程式庫，hello 分區對應管理員是分區對應的集合。 hello 所管理的資料**ShardMapManager**執行個體就會保留在三個位置： 

1. **全域分區對應 (GSM)**： 您指定資料庫 tooserve 為 hello 所有分區對應及對應的儲存機制。 特殊的資料表和預存程序會自動建立 toomanage hello 資訊。 這通常是一個小型資料庫，以及少量的存取，並不應該使用 hello 應用程式的其他需求。 hello 資料表是在特殊結構描述中名為**__ShardManagement**。 
2. **分區對應 (LSM)**： 您指定的 toobe 分區是修改 toocontain，數個小型資料表和包含與管理分區對應資訊的特定 toothat 分區的特殊預存程序的每個資料庫。 這項資訊是與 hello GSM 中的 hello 資訊多餘的它允許 hello 應用程式快取 toovalidate 分區對應資訊而不在 hello GSM; 中放置任何負載hello 應用程式會使用 hello LSM toodetermine，如果快取的對應仍然有效。 hello 資料表上每個分區 LSM 還有 hello 結構描述中的對應 toohello **__ShardManagement**。
3. **應用程式快取**：每個存取 **ShardMapManager** 物件的應用程式執行個體會維護其對應的本機記憶體內部快取。 它會儲存最近擷取的路由資訊。 

## <a name="constructing-a-shardmapmanager"></a>建構 ShardMapManager
**ShardMapManager** 物件是使用 [Factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) 模式所建構。 hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** 方法採用 hello 形式的認證 （包括 hello 伺服器名稱和資料庫名稱保留 hello GSM） **ConnectionString**和傳回的執行個體**ShardMapManager**。  

**請注意：** hello **ShardMapManager**應該具現化一次只能每個應用程式的 hello 初始化程式碼內的應用程式網域。 建立額外的執行個體的 ShardMapManager hello 中相同的 appdomain 中，會導致增加的記憶體和 CPU 的使用率 hello 應用程式。 **ShardMapManager** 可以包含任意數目的分區對應。 雖然單一分區對應可能足夠用於許多應用程式，但有時幾組不同的資料庫會用於不同的結構描述或做為特殊用途；在這些情況下，最好使用多個分區對應。 

在這段程式碼，應用程式會嘗試在現有 tooopen **ShardMapManager**以 hello [TryGetSqlShardMapManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)。  如果物件，代表全域**ShardMapManager** (GSM) 不相符，尚未存在 hello 資料庫內，hello 用戶端程式庫會建立它們那里使用 hello [CreateSqlShardMapManager 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)。

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

或者，您可以使用 Powershell toocreate 新的分區對應管理員。 範例請見 [這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。

## <a name="get-a-rangeshardmap-or-listshardmap"></a>取得 RangeShardMap 或 ListShardMap
在建立之後分區對應管理員，您可以取得 hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx)或[ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx)使用 hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)，hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)，或使用 hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)方法。

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

### <a name="shard-map-administration-credentials"></a>分區對應系統管理認證
管理和操作分區對應的應用程式會不同於使用 hello 分區對應 tooroute 連線。 

tooadminister 分區對應 （新增或變更分區，分區對應中，分區對應等） 必須具現化 hello **ShardMapManager**使用**認證具有讀取/寫入權限，這兩個 hello GSM 資料庫上與每個做為分區化資料庫**。 hello 認證必須允許針對這兩個 hello 中的 hello 資料表寫入 GSM 和 LSM 分區對應資訊是輸入或變更，以及與建立新的分區 LSM 資料表時。  

請參閱[使用 tooaccess hello 彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。

### <a name="only-metadata-affected"></a>只影響中繼資料
用於填入或變更 hello 方法**ShardMapManager**資料不會改變 hello 使用者資料儲存在本身的 hello 分區中。 比方說，這類方法**CreateShard**， **DeleteShard**， **UpdateMapping**等影響 hello 分區對應僅為中繼資料。 請勿移除、 新增或變更包含在 hello 分區中的使用者資料。 相反地，這些方法是使用設計的 toobe 搭配不同的作業執行 toocreate 或移除實際的資料庫，或該移動的資料列從一個分區 tooanother toorebalance 分區化的環境。  (hello**分割合併**彈性資料庫工具所隨附的工具會使用這些 Api，以及協調分區之間的實際資料移動。)請參閱[調整使用 hello 彈性資料庫分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)。

## <a name="populating-a-shard-map-example"></a>填入分區對應範例
作業 toopopulate 特定分區對應的範例順序如下所示。 hello 程式碼執行下列步驟： 

1. 在分區對應管理員內建立新的分區對應。 
2. 兩個不同分區的 hello 中繼資料會加入 toohello 分區對應。 
3. 加入各種不同的索引鍵範圍的對應，並 hello 整體 hello 分區對應會顯示的內容。 

hello 程式碼會寫入，以便可以重新執行 hello 方法，如果發生錯誤。 每個要求會測試是否分區或對應已經存在，然後再嘗試 toocreate 它。 hello 程式碼會假設資料庫命名為**sample_shard_0**， **sample_shard_1**和**sample_shard_2** hello 字串所參考的伺服器中已經建立**shardServer**。 

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

因為替代，您可以使用 PowerShell 指令碼 tooachieve hello 結果相同。 有些 hello 範例 PowerShell 範例[這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。     

一旦填入分區對應之後，資料存取應用程式可以建立，或調整 toowork 與 hello 地圖。 填入或操作 hello 對應需要不會發生一次，直到**對應配置**需要 toochange。  

## <a name="data-dependent-routing"></a>資料相依路由
hello 分區對應管理員將最用於需要資料庫連接 tooperform hello 應用程式特定資料作業的應用程式。 這些連線必須與 hello 正確的資料庫相關聯。 這稱為 **資料相依路由**。 對於這些應用程式中，具現化 hello 原廠使用 hello GSM 資料庫具有唯讀存取權的認證從分區對應管理員物件。 個別的更新版本的連線要求提供連線 toohello 適當的分區化資料庫所需的認證。

請注意，這些應用程式 (使用**ShardMapManager**開啟具有唯讀的認證) toohello 對應的無法進行變更。 針對這些需求，請建立管理專用應用程式或 PowerShell 指令碼，以提供稍早所述較高權限的認證。 請參閱[使用 tooaccess hello 彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。

如需詳細資訊，請參閱 [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)。 

## <a name="modifying-a-shard-map"></a>修改分區對應
您可以使用不同方式來變更分區對應。 所有 hello 下列方法修改 hello 中繼資料描述 hello 分區和他們的對應，但他們不實際修改 hello 分區內的資料也請勿在建立或刪除 hello 實際的資料庫。  某些 hello hello 分區對應如下所述的作業可能需要 toobe 協調的實際移動資料，或者加入和移除資料庫做為分區的系統管理動作。

這些方法一起當作 hello 建置組塊可用於修改 hello 整體分佈的分區化資料庫環境中的資料。  

* tooadd 或移除分區： 使用 **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** 和 **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** 的 hello [Shardmap 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)。 
  
    hello 伺服器和資料庫代表 hello 目標分區必須已經存在的這些作業 tooexecute。 這些方法只能在 hello 分區對應中的中繼資料本身，hello 資料庫上沒有任何影響。
* 對應 toohello 分區 toocreate 或移除點或範圍： 使用 **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**，  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** 的 hello[RangeShardMapping 類別](https://msdn.microsoft.com/library/azure/dn807318.aspx)，和 **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** 的 hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    許多不同時間點或範圍可以對應的 toohello 相同分區。 這些方法只會影響中繼資料 - 不會影響分區中可能已經存在的任何資料。 如果資料需要從 hello 中順序 toobe 與一致的資料庫中移除的 toobe **DeleteMapping**作業，您將需要 tooperform 這些作業分別但搭配使用這些方法。  
* toosplit 兩種、 或合併成一個相鄰的範圍到現有的範圍： 使用 **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** 和 **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**。  
  
    請注意，分割及合併作業**不會變更 hello 分區 toowhich 機碼值會對應**。 分割的現有範圍分成兩個部分，但會保留兩種形式對應 toohello 相同分區。 已對應的 toohello 的兩個相鄰範圍上運作的合併相同的分區，聯合它們成單一範圍。  hello 的點或分區之間本身範圍移動需要 toobe 協調使用**UpdateMapping**搭配實際的資料移動。  您可以使用 hello**分割/合併**屬於彈性資料庫的服務需要移動時，工具 toocoordinate 分區對應變更的資料移動。 
* toore 對應 （或移動） 個別點或範圍 toodifferent 分區： 使用 **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**。  
  
    因為資料可能需要從一個分區 tooanother 中與一致的順序 toobe 移 toobe **UpdateMapping**作業，您將需要 tooperform 該移動分開但搭配使用這些方法。
* 線上和離線 tootake 對應： 使用 **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** 和 **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello 的線上狀態對應。 
  
    只有當對應處於「離線」狀態時，才允許分區對應上的某些作業，包括 **UpdateMapping** 和 **DeleteMapping**。 對應離線時，根據該對應中包含的索引鍵來提出資料相依要求會傳回錯誤。 此外，範圍第一次離線時，所有連線 toohello 影響分區會自動都終止順序 tooprevent 不一致或不完整結果的查詢，針對要變更的範圍中。 

對應是 .Net 中不可變的物件。  Hello 上述方法，變更對應的所有也會使程式碼中的任何參考 toothem。 toomake it 更容易 tooperform 順序的變更對應的狀態，變更對應的 hello 方法的所有作業都會傳回新對應的參考，讓作業可以鏈結。 比方說，現有的對應中包含 hello 金鑰 25 shardmap sm toodelete，您可以執行下列的 hello: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>加入分區
應用程式通常需要 toosimply 新增分區 toohandle 資料應從新的索引鍵或索引鍵範圍，分區對應已經存在。 比方說，分區化應用程式的租用戶識別碼可能需要 tooprovision 新的分區，新的租用戶，或資料分區化每月可能需要新的分區，佈建的每個新月份的 hello 起始之前。 

如果 hello 新索引鍵值的範圍還不屬於現有的對應並不會移動資料是必要的它是非常簡單 tooadd hello 新的分區，並將 hello 新的金鑰或範圍 toothat 分區產生關聯。 如需有關加入新分區的詳細資訊，請參閱 [加入新的分區](sql-database-elastic-scale-add-a-shard.md)。

不過，需要移動資料的情況下，hello 分割合併工具是分區搭配 hello 必要分區對應更新之間的所需的 tooorchestrate hello 資料移動。 如需使用詳細資訊 hello yool 分割合併，請參閱 <<c0> [ 分割合併的概觀](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
