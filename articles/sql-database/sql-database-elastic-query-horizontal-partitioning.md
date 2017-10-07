---
title: "向外延展雲端資料庫之間的 aaaReporting |Microsoft 文件"
description: "如何透過水平資料分割的彈性查詢 tooset"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>跨相應放大的雲端資料庫報告 (預覽)
![跨分區查詢][1]

分區化資料庫跨相應放大的資料層發佈資料列。 hello 結構描述是在參與資料庫，也就是水平資料分割上完全相同。 使用彈性查詢，您可以建立跨越分區化資料庫中所有資料庫的報告。

如需快速啟動，請參閱 [跨相應放大的雲端資料庫報告](sql-database-elastic-query-getting-started.md)。

如需非分區化資料庫，請參閱 [對不同結構描述的雲端資料庫執行查詢](sql-database-elastic-query-vertical-partitioning.md)。 

## <a name="prerequisites"></a>必要條件
* 建立使用 hello 彈性資料庫用戶端程式庫的分區對應。 請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。 使用中的 hello 範例應用程式或者[彈性資料庫 tools 快速入門](sql-database-elastic-scale-get-started.md)。
* 或者，請參閱[移轉現有的資料庫 tooscaled 外資料庫](sql-database-elastic-convert-to-use-elastic-tools.md)。
* hello 使用者必須擁有 ALTER ANY EXTERNAL DATA SOURCE 權限。 此權限會包含 hello ALTER DATABASE 權限。
* ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。

## <a name="overview"></a>概觀
這些陳述式 hello 彈性查詢資料庫中建立您的分區化的資料層 hello 中繼資料表示。 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [建立資料庫範圍認證](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 建立資料庫範圍的主要金鑰和認證
hello 認證會使用 hello 彈性查詢 tooconnect tooyour 遠端資料庫。  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> 請確定該 hello *"\<username\>"*不包含任何*"@servername"*後置詞。 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 建立外部資料來源
語法：

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>範例
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

擷取目前的外部資料來源 hello 清單： 

    select * from sys.external_data_sources; 

hello 外部資料來源參考分區對應。 Hello 外部資料來源與 hello 基礎分區對應 tooenumerate hello 資料庫參與 hello 資料層，然後會使用彈性的查詢。 hello 相同認證是使用的 tooread hello 分區對應，而且 tooaccess hello 彈性的查詢處理期間 hello hello 分區上的資料。 

## <a name="13-create-external-tables"></a>1.3 建立外部資料表
語法：  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**範例**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

擷取 hello 目前資料庫中的 hello 外部資料表清單： 

    SELECT * from sys.external_tables; 

toodrop 外部資料表：

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>備註
hello 資料\_來源子句會定義用於 hello 外部資料表的 hello 外部資料來源 （分區對應）。  

hello 結構描述\_名稱和物件\_名稱子句會將 hello 外部資料表定義 tooa 資料表不同的結構描述中的對應。 Hello hello 遠端物件的結構描述如果省略，則會假設 toobe"dbo"，而會假設其名稱所定義的 toobe 相同 toohello 外部資料表名稱。 這是適用於遠端資料表的名稱，hello 已被 hello 資料庫中您要 toocreate hello 外部資料表。 比方說，您想 toodefine 外部資料表 tooget 目錄檢視的彙總檢視，或在向外延展的資料上的 Dmv 層。 由於目錄檢視和 Dmv 已存在於本機上，您無法使用其 hello 外部資料表定義的名稱。 相反地，使用不同的名稱和使用 hello 目錄檢視的或 hello hello 結構描述中的 DMV 名稱\_名稱和/或物件\_名稱子句。 （請參閱以下的 hello 範例）。 

hello 發佈子句指定 hello 這個資料表所使用的資料分佈。 hello 查詢處理器會利用 hello hello 發佈子句 toobuild hello 最有效率的查詢計劃中提供的資訊。  

1. **分區化**表示 hello 資料庫之間的資料水平分割。 hello hello 資料分佈的資料分割索引鍵的 hello **< sharding_column_name >**參數。
2. **複寫**表示 hello 資料表的相同複本都存在於每個資料庫上。 它是您的責任 tooensure hello 複本跨 hello 資料庫完全相同。
3. **ROUND\_循環配置資源**表示該 hello 資料表水平資料分割使用應用程式相依發佈方法。 

**資料層參考**: hello 外部資料表 DDL 參考 tooan 外部資料來源。 hello 外部資料來源指定分區對應您的資料層中的所有 hello 資料庫時提供使用 hello 資訊必要 toolocate hello 外部資料表。 

### <a name="security-considerations"></a>安全性考量
使用者具有存取 toohello 外部資料表會自動存取 toohello 基礎遠端的資料表在 hello hello 外部資料來源定義中提供的認證。 避免不想要透過 hello hello 外部資料來源認證的權限提高。 對外部資料表使用「授與」或「撤銷」，就像它是一般的資料表一樣。  

一旦您已定義外部資料來源和外部資料表，現在您可以對外部資料表使用完整的 T-SQL。

## <a name="example-querying-horizontal-partitioned-databases"></a>範例︰查詢水平資料分割的資料庫
hello 下列查詢會執行三種方式之間的聯結倉儲、 訂單及訂單產品線，並使用數個彙總和選擇性篩選。 它會假設 （1） 水平資料分割 （分區化） 和 （2），倉儲、 訂單及訂單產品線都由 hello 倉儲識別碼資料行中，分區化 hello 彈性查詢可共置在 hello 分區 hello 聯結和處理 hello 上 hello hello 查詢一部分高度耗費資源以平行方式分區。 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>用於遠端 T-SQL 執行的預存程序：sp\_execute_remote
彈性查詢也會介紹可直接存取 toohello 分區的預存程序。 hello 預存程序稱為[sp\_執行\_遠端](https://msdn.microsoft.com/library/mt703714)而且可以是使用的 tooexecute 遠端預存程序或 hello 遠端資料庫上的 T-SQL 程式碼。 它會採用下列參數的 hello: 

* 資料來源名稱 (nvarchar): hello hello 類型 RDBMS 外部資料來源名稱。 
* 查詢 (nvarchar): hello T-SQL 查詢 toobe 在每個分區上執行。 
* 參數宣告 (nvarchar)-選擇性： hello 查詢參數 （例如 sp_executesql) 中使用的 hello 參數的資料型別定義的字串。 
* 參數值清單 - 選用：以逗號分隔的參數值清單 (如 sp_executesql)。

hello sp\_執行\_遠端使用 hello hello 引動過程參數 tooexecute hello hello 遠端資料庫上給定 T-SQL 陳述式中提供的外部資料來源。 它會使用 hello hello 外部資料來源 tooconnect toohello shardmap manager 資料庫和 hello 遠端資料庫的認證。  

範例： 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>工具的連線能力
使用一般 SQL Server 連接字串 tooconnect 您的應用程式、 BI 和資料整合工具 toohello 資料庫外部資料表定義。 請確定 SQL Server 可支援做為您的工具的資料來源。 然後參考 hello 彈性查詢資料庫，像任何其他 SQL Server 連接資料庫 toohello 工具，並使用從您的工具或應用程式的外部資料表，就如同本機資料表。 

## <a name="best-practices"></a>最佳作法
* 請確定該 hello 彈性查詢端點的資料庫具有存取 toohello shardmap 資料庫和透過 SQL DB 防火牆的 hello 所有分區。  
* 驗證或強制執行 hello hello 外部資料表所定義的資料分佈。 如果您的實際資料散發 hello 散發在資料表定義中指定不同，您的查詢可能會產生非預期的結果。 
* 彈性查詢目前不會執行分區刪除時透過 hello 分區化索引鍵述詞可讓它 toosafely 排除特定的分區處理。
* 彈性查詢最適合查詢其中完成大部分的 hello 計算上 hello 分區。 您通常包含選擇性的篩選器述詞，可評估 hello 最佳查詢效能 hello 分區或聯結上透過取得 hello 資料分割索引鍵可執行的資料分割對齊的方式在所有分區。 其他的查詢模式可能需要 tooload 大量資料從 hello 分區 toohello 前端節點和執行效能很差

## <a name="next-steps"></a>後續步驟

* 如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。
* 若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。
* 如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)
* 如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。
* 如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
