---
title: "使用彈性資料庫工具的分區的 aaaAdding |Microsoft 文件"
description: "如何設定 toouse Elastic Scale Api tooadd 新分區 tooa 分區。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>使用彈性資料庫工具加入分區
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd 新範圍或金鑰的分區
應用程式通常需要 toosimply 新增分區 toohandle 資料應從新的索引鍵或索引鍵範圍，分區對應已經存在。 比方說，分區化應用程式的租用戶識別碼可能需要 tooprovision 新的分區，新的租用戶，或資料分區化每月可能需要新的分區，佈建的每個新月份的 hello 起始之前。 

如果 hello 新索引鍵值的範圍還不屬於現有，是對應的非常簡單 tooadd hello 新分區和關聯 hello 新索引鍵或範圍 toothat 的分區。 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>範例： 新增分區和其範圍 tooan 現有分區對應
這個範例會使用 hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)， [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\))方法，並建立執行個體的 hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.)類別。 在 [hello 範例資料庫] 下，名為**sample_shard_2** ，且已建立所有必要的結構描述物件在其內部 toohold 範圍 [300、 400）。  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


或者，您可以使用 Powershell toocreate 新的分區對應管理員。 範例請見 [這裡](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd 空白的組件的現有範圍的分區
在某些情況下，您會有資料行已經對應範圍 tooa 分區，與部分填入資料，但是現在想即將發行的資料 toobe 導向的 tooa 不同分區。 比方說，您分區依日排列的範圍，而且已經已經配置 50 天 tooa 分區，但要在一天 24，未來的資料 tooland 不同分區中。 hello 彈性資料庫[分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)才能執行此作業，但如果資料移動，不必要 （例如 [25，50 天 hello 範圍的資料），也就是 25 天 （含) too50 獨佔，尚未存在) 您可以執行這完全使用直接 hello 分區對應管理 Api。

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>範例： 分割範圍和指派 hello 空白部分 tooa 新增分區
已建立名為 "sample_shard_2" 的資料庫，及其中所有必要的結構描述物件。  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**重要**： 如果您是有些 hello 的範圍是空的 hello 更新對應僅使用這項技術。  上述的 hello 方法不會檢查正在移動的 hello 範圍的資料，因此最適合 tooinclude 會檢查您的程式碼中。  如果要移動的 hello 範圍中存在的資料列，hello 實際資料散發會不符合 hello 更新的分區對應。 使用 hello[分割合併工具](sql-database-elastic-scale-overview-split-and-merge.md)tooperform hello 作業改為在這些情況下。  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

