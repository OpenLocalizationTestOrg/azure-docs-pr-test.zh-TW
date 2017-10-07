---
title: "aaaMigrate 現有資料庫 tooscale 外 |Microsoft 文件"
description: "藉由建立分區對應管理員轉換分區化資料庫 toouse 彈性資料庫工具"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>移轉現有的資料庫 tooscale 外
輕鬆地管理您現有向外延展分區化資料庫時使用 Azure SQL Database 資料庫工具 (例如 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md))。 您必須先轉換現有的資料庫 toouse hello 一組[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)。 

## <a name="overview"></a>概觀
toomigrate 現有的分區化資料庫： 

1. 準備 hello[分區對應管理員資料庫](sql-database-elastic-scale-shard-map-management.md)。
2. 建立 hello 分區對應。
3. 準備 hello 個別分區。  
4. 新增對應 toohello 分區對應。

這些技術可以使用任一 hello 實作[.NET Framework 用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)，或 hello PowerShell 指令碼，請參閱[Azure SQL DB 彈性資料庫工具指令碼](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。 hello 範例使用 hello PowerShell 指令碼。

如需 hello ShardMapManager 的詳細資訊，請參閱[分區對應管理](sql-database-elastic-scale-shard-map-management.md)。 如需 hello 彈性資料庫工具的概觀，請參閱[彈性資料庫功能概觀](sql-database-elastic-scale-introduction.md)。

## <a name="prepare-hello-shard-map-manager-database"></a>準備 hello 分區對應管理員資料庫
hello 分區對應管理員是包含 hello 資料 toomanage 向外延展資料庫的特殊資料庫。 您可以使用現有的資料庫，或建立新的資料庫。 請注意，資料庫作為分區對應管理員不應 hello 相同資料庫作為分區。 也請注意 hello PowerShell 指令碼不會為您建立 hello 資料庫。 

## <a name="step-1-create-a-shard-map-manager"></a>步驟 1︰建立分區對應管理員
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>tooretrieve hello 分區對應管理員
在建立之後，您可以擷取與這個指令程式的 hello 分區對應管理員。 每次需要 toouse hello ShardMapManager 物件，則需要這個步驟。

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>步驟 2： 建立 hello 分區對應
您必須選取分區對應 toocreate hello 類型。 hello 選擇取決於 hello 資料庫架構： 

1. 每個資料庫的單一租用戶 (條款，請參閱 hello[詞彙](sql-database-elastic-scale-glossary.md)。) 
2. 每個資料庫的多個租用戶 (兩種類型)︰
   1. 清單對應
   2. 範圍對應

針對單一租用戶模型，建立 **清單對應** 分區對應。 hello 單一租用戶模型會指派一個資料庫，每個租用戶。 這是適用於 SaaS 開發人員的有效模式，因為它會簡化管理。

![清單對應][1]

hello 多租用戶模型會指派數個租用戶 tooa 單一資料庫 （和分散多個資料庫的租用戶的群組）。 當您希望產生每個租用戶 toohave 小型資料需要使用此模型。 在此模型中，我們會將指派租用戶 tooa 資料庫使用的範圍**範圍對應**。 

![範圍對應][2]

您可以實作多租用戶資料庫模型，使用或*清單對應*tooassign 多個租用戶 tooa 單一資料庫。 例如，DB1 是租用戶識別碼 1 和 5，請使用的 toostore 的資訊，而 DB2 儲存 7 租用戶和租用戶 10 的資料。 

![單一資料庫上的多個租用戶][3] 

**根據您的選擇，選擇下列其中一個選項︰**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>選項 1︰建立清單對應的分區對應
建立使用 hello ShardMapManager 物件分區對應。 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>選項 2︰建立範圍對應的分區對應
請注意該 tooutilize 此對應模式、 租用戶的識別碼值需要 toobe 連續範圍，而它是 hello 範圍中的可接受 toohave 間隔藉由建立 hello 資料庫時，只略過 hello 範圍。

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>選項 3︰單一資料庫上的清單對應
設定此模式也需要建立清單對應，如步驟 2，選項 1 所示。

## <a name="step-3-prepare-individual-shards"></a>步驟 3︰準備個別分區
加入每個分區 （資料庫） toohello 分區對應管理員。 這會準備 hello 個別資料庫儲存對應資訊。 在每個分區上執行此方法。

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>步驟 4︰新增對應
對應的 hello 加法取決於您所建立的分區對應 hello 種類。 如果已建立清單對應，則會新增清單對應。 如果已建立範圍對應，則會新增範圍對應。

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>清單對應的選項 1： 對應 hello 資料
Hello 資料對應每個租用戶加入清單的對應。  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>選項 2： 地圖 hello 資料範圍的對應
加入所有的 hello 租用戶識別碼範圍-資料庫關聯的 hello 範圍對應：

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>步驟 4 選項 3: hello 資料對應的單一資料庫上的多個租用戶
每個租用戶，執行新增 ListMapping hello （選項 1，上方）。 

## <a name="checking-hello-mappings"></a>檢查 hello 對應
您可以使用下列命令查詢 hello 現有分區和與其相關聯的 hello 對應的相關資訊：  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>摘要
當您完成 hello 安裝程式時，您可以開始 toouse hello 彈性資料庫用戶端程式庫。 您也可以使用[資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)和[多分區查詢](sql-database-elastic-scale-multishard-querying.md)。

## <a name="next-steps"></a>後續步驟
取得從 hello PowerShell 指令碼[Azure SQL DB 彈性資料庫工具 sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db)。

hello 工具也會在 GitHub 上： [Azure/彈性-db-tools](https://github.com/Azure/elastic-db-tools)。

使用來自多租用戶模型 tooa 單一租用戶模型 hello 分割合併工具 toomove 資料 tooor。 請參閱 [分割合併工具](sql-database-elastic-scale-get-started.md)。

## <a name="additional-resources"></a>其他資源
如需多租用戶型軟體即服務 (SaaS) 資料庫應用程式的常見資料架構模式的資訊，請參閱 [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)。

## <a name="questions-and-feature-requests"></a>問題和功能要求
如有問題，請聯繫 toous 上 hello [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)和功能的要求，請將它們加入 toohello [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

