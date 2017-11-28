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
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="6491c-103">跨相應放大的雲端資料庫報告 (預覽)</span><span class="sxs-lookup"><span data-stu-id="6491c-103">Reporting across scaled-out cloud databases (preview)</span></span>
![跨分區查詢][1]

<span data-ttu-id="6491c-105">分區化資料庫跨相應放大的資料層發佈資料列。</span><span class="sxs-lookup"><span data-stu-id="6491c-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="6491c-106">hello 結構描述是在參與資料庫，也就是水平資料分割上完全相同。</span><span class="sxs-lookup"><span data-stu-id="6491c-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="6491c-107">使用彈性查詢，您可以建立跨越分區化資料庫中所有資料庫的報告。</span><span class="sxs-lookup"><span data-stu-id="6491c-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="6491c-108">如需快速啟動，請參閱 [跨相應放大的雲端資料庫報告](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="6491c-109">如需非分區化資料庫，請參閱 [對不同結構描述的雲端資料庫執行查詢](sql-database-elastic-query-vertical-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6491c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6491c-110">Prerequisites</span></span>
* <span data-ttu-id="6491c-111">建立使用 hello 彈性資料庫用戶端程式庫的分區對應。</span><span class="sxs-lookup"><span data-stu-id="6491c-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="6491c-112">請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="6491c-113">使用中的 hello 範例應用程式或者[彈性資料庫 tools 快速入門](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="6491c-114">或者，請參閱[移轉現有的資料庫 tooscaled 外資料庫](sql-database-elastic-convert-to-use-elastic-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="6491c-115">hello 使用者必須擁有 ALTER ANY EXTERNAL DATA SOURCE 權限。</span><span class="sxs-lookup"><span data-stu-id="6491c-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="6491c-116">此權限會包含 hello ALTER DATABASE 權限。</span><span class="sxs-lookup"><span data-stu-id="6491c-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="6491c-117">ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="6491c-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="6491c-118">概觀</span><span class="sxs-lookup"><span data-stu-id="6491c-118">Overview</span></span>
<span data-ttu-id="6491c-119">這些陳述式 hello 彈性查詢資料庫中建立您的分區化的資料層 hello 中繼資料表示。</span><span class="sxs-lookup"><span data-stu-id="6491c-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="6491c-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="6491c-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="6491c-121">建立資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="6491c-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="6491c-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="6491c-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="6491c-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="6491c-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="6491c-124">1.1 建立資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="6491c-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="6491c-125">hello 認證會使用 hello 彈性查詢 tooconnect tooyour 遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="6491c-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="6491c-126">請確定該 hello *"\<username\>"*不包含任何*"@servername"*後置詞。</span><span class="sxs-lookup"><span data-stu-id="6491c-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="6491c-127">1.2 建立外部資料來源</span><span class="sxs-lookup"><span data-stu-id="6491c-127">1.2 Create external data sources</span></span>
<span data-ttu-id="6491c-128">語法：</span><span class="sxs-lookup"><span data-stu-id="6491c-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="6491c-129">範例</span><span class="sxs-lookup"><span data-stu-id="6491c-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="6491c-130">擷取目前的外部資料來源 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="6491c-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="6491c-131">hello 外部資料來源參考分區對應。</span><span class="sxs-lookup"><span data-stu-id="6491c-131">hello external data source references your shard map.</span></span> <span data-ttu-id="6491c-132">Hello 外部資料來源與 hello 基礎分區對應 tooenumerate hello 資料庫參與 hello 資料層，然後會使用彈性的查詢。</span><span class="sxs-lookup"><span data-stu-id="6491c-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="6491c-133">hello 相同認證是使用的 tooread hello 分區對應，而且 tooaccess hello 彈性的查詢處理期間 hello hello 分區上的資料。</span><span class="sxs-lookup"><span data-stu-id="6491c-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="6491c-134">1.3 建立外部資料表</span><span class="sxs-lookup"><span data-stu-id="6491c-134">1.3 Create external tables</span></span>
<span data-ttu-id="6491c-135">語法：</span><span class="sxs-lookup"><span data-stu-id="6491c-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="6491c-136">**範例**</span><span class="sxs-lookup"><span data-stu-id="6491c-136">**Example**</span></span>

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

<span data-ttu-id="6491c-137">擷取 hello 目前資料庫中的 hello 外部資料表清單：</span><span class="sxs-lookup"><span data-stu-id="6491c-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="6491c-138">toodrop 外部資料表：</span><span class="sxs-lookup"><span data-stu-id="6491c-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="6491c-139">備註</span><span class="sxs-lookup"><span data-stu-id="6491c-139">Remarks</span></span>
<span data-ttu-id="6491c-140">hello 資料\_來源子句會定義用於 hello 外部資料表的 hello 外部資料來源 （分區對應）。</span><span class="sxs-lookup"><span data-stu-id="6491c-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="6491c-141">hello 結構描述\_名稱和物件\_名稱子句會將 hello 外部資料表定義 tooa 資料表不同的結構描述中的對應。</span><span class="sxs-lookup"><span data-stu-id="6491c-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="6491c-142">Hello hello 遠端物件的結構描述如果省略，則會假設 toobe"dbo"，而會假設其名稱所定義的 toobe 相同 toohello 外部資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6491c-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="6491c-143">這是適用於遠端資料表的名稱，hello 已被 hello 資料庫中您要 toocreate hello 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="6491c-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="6491c-144">比方說，您想 toodefine 外部資料表 tooget 目錄檢視的彙總檢視，或在向外延展的資料上的 Dmv 層。</span><span class="sxs-lookup"><span data-stu-id="6491c-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="6491c-145">由於目錄檢視和 Dmv 已存在於本機上，您無法使用其 hello 外部資料表定義的名稱。</span><span class="sxs-lookup"><span data-stu-id="6491c-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="6491c-146">相反地，使用不同的名稱和使用 hello 目錄檢視的或 hello hello 結構描述中的 DMV 名稱\_名稱和/或物件\_名稱子句。</span><span class="sxs-lookup"><span data-stu-id="6491c-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="6491c-147">（請參閱以下的 hello 範例）。</span><span class="sxs-lookup"><span data-stu-id="6491c-147">(See hello example below.)</span></span> 

<span data-ttu-id="6491c-148">hello 發佈子句指定 hello 這個資料表所使用的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="6491c-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="6491c-149">hello 查詢處理器會利用 hello hello 發佈子句 toobuild hello 最有效率的查詢計劃中提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="6491c-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="6491c-150">**分區化**表示 hello 資料庫之間的資料水平分割。</span><span class="sxs-lookup"><span data-stu-id="6491c-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="6491c-151">hello hello 資料分佈的資料分割索引鍵的 hello **< sharding_column_name >**參數。</span><span class="sxs-lookup"><span data-stu-id="6491c-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="6491c-152">**複寫**表示 hello 資料表的相同複本都存在於每個資料庫上。</span><span class="sxs-lookup"><span data-stu-id="6491c-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="6491c-153">它是您的責任 tooensure hello 複本跨 hello 資料庫完全相同。</span><span class="sxs-lookup"><span data-stu-id="6491c-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="6491c-154">**ROUND\_循環配置資源**表示該 hello 資料表水平資料分割使用應用程式相依發佈方法。</span><span class="sxs-lookup"><span data-stu-id="6491c-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="6491c-155">**資料層參考**: hello 外部資料表 DDL 參考 tooan 外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="6491c-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="6491c-156">hello 外部資料來源指定分區對應您的資料層中的所有 hello 資料庫時提供使用 hello 資訊必要 toolocate hello 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="6491c-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="6491c-157">安全性考量</span><span class="sxs-lookup"><span data-stu-id="6491c-157">Security considerations</span></span>
<span data-ttu-id="6491c-158">使用者具有存取 toohello 外部資料表會自動存取 toohello 基礎遠端的資料表在 hello hello 外部資料來源定義中提供的認證。</span><span class="sxs-lookup"><span data-stu-id="6491c-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="6491c-159">避免不想要透過 hello hello 外部資料來源認證的權限提高。</span><span class="sxs-lookup"><span data-stu-id="6491c-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="6491c-160">對外部資料表使用「授與」或「撤銷」，就像它是一般的資料表一樣。</span><span class="sxs-lookup"><span data-stu-id="6491c-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="6491c-161">一旦您已定義外部資料來源和外部資料表，現在您可以對外部資料表使用完整的 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="6491c-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="6491c-162">範例︰查詢水平資料分割的資料庫</span><span class="sxs-lookup"><span data-stu-id="6491c-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="6491c-163">hello 下列查詢會執行三種方式之間的聯結倉儲、 訂單及訂單產品線，並使用數個彙總和選擇性篩選。</span><span class="sxs-lookup"><span data-stu-id="6491c-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="6491c-164">它會假設 （1） 水平資料分割 （分區化） 和 （2），倉儲、 訂單及訂單產品線都由 hello 倉儲識別碼資料行中，分區化 hello 彈性查詢可共置在 hello 分區 hello 聯結和處理 hello 上 hello hello 查詢一部分高度耗費資源以平行方式分區。</span><span class="sxs-lookup"><span data-stu-id="6491c-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="6491c-165">用於遠端 T-SQL 執行的預存程序：sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="6491c-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="6491c-166">彈性查詢也會介紹可直接存取 toohello 分區的預存程序。</span><span class="sxs-lookup"><span data-stu-id="6491c-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="6491c-167">hello 預存程序稱為[sp\_執行\_遠端](https://msdn.microsoft.com/library/mt703714)而且可以是使用的 tooexecute 遠端預存程序或 hello 遠端資料庫上的 T-SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="6491c-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="6491c-168">它會採用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="6491c-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="6491c-169">資料來源名稱 (nvarchar): hello hello 類型 RDBMS 外部資料來源名稱。</span><span class="sxs-lookup"><span data-stu-id="6491c-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="6491c-170">查詢 (nvarchar): hello T-SQL 查詢 toobe 在每個分區上執行。</span><span class="sxs-lookup"><span data-stu-id="6491c-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="6491c-171">參數宣告 (nvarchar)-選擇性： hello 查詢參數 （例如 sp_executesql) 中使用的 hello 參數的資料型別定義的字串。</span><span class="sxs-lookup"><span data-stu-id="6491c-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="6491c-172">參數值清單 - 選用：以逗號分隔的參數值清單 (如 sp_executesql)。</span><span class="sxs-lookup"><span data-stu-id="6491c-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="6491c-173">hello sp\_執行\_遠端使用 hello hello 引動過程參數 tooexecute hello hello 遠端資料庫上給定 T-SQL 陳述式中提供的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="6491c-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="6491c-174">它會使用 hello hello 外部資料來源 tooconnect toohello shardmap manager 資料庫和 hello 遠端資料庫的認證。</span><span class="sxs-lookup"><span data-stu-id="6491c-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="6491c-175">範例：</span><span class="sxs-lookup"><span data-stu-id="6491c-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="6491c-176">工具的連線能力</span><span class="sxs-lookup"><span data-stu-id="6491c-176">Connectivity for tools</span></span>
<span data-ttu-id="6491c-177">使用一般 SQL Server 連接字串 tooconnect 您的應用程式、 BI 和資料整合工具 toohello 資料庫外部資料表定義。</span><span class="sxs-lookup"><span data-stu-id="6491c-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="6491c-178">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="6491c-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="6491c-179">然後參考 hello 彈性查詢資料庫，像任何其他 SQL Server 連接資料庫 toohello 工具，並使用從您的工具或應用程式的外部資料表，就如同本機資料表。</span><span class="sxs-lookup"><span data-stu-id="6491c-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="6491c-180">最佳作法</span><span class="sxs-lookup"><span data-stu-id="6491c-180">Best practices</span></span>
* <span data-ttu-id="6491c-181">請確定該 hello 彈性查詢端點的資料庫具有存取 toohello shardmap 資料庫和透過 SQL DB 防火牆的 hello 所有分區。</span><span class="sxs-lookup"><span data-stu-id="6491c-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="6491c-182">驗證或強制執行 hello hello 外部資料表所定義的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="6491c-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="6491c-183">如果您的實際資料散發 hello 散發在資料表定義中指定不同，您的查詢可能會產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="6491c-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="6491c-184">彈性查詢目前不會執行分區刪除時透過 hello 分區化索引鍵述詞可讓它 toosafely 排除特定的分區處理。</span><span class="sxs-lookup"><span data-stu-id="6491c-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="6491c-185">彈性查詢最適合查詢其中完成大部分的 hello 計算上 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="6491c-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="6491c-186">您通常包含選擇性的篩選器述詞，可評估 hello 最佳查詢效能 hello 分區或聯結上透過取得 hello 資料分割索引鍵可執行的資料分割對齊的方式在所有分區。</span><span class="sxs-lookup"><span data-stu-id="6491c-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="6491c-187">其他的查詢模式可能需要 tooload 大量資料從 hello 分區 toohello 前端節點和執行效能很差</span><span class="sxs-lookup"><span data-stu-id="6491c-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="6491c-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6491c-188">Next steps</span></span>

* <span data-ttu-id="6491c-189">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="6491c-190">若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="6491c-191">如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="6491c-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="6491c-192">如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6491c-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="6491c-193">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="6491c-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
