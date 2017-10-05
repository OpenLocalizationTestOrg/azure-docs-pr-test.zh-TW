---
title: "跨相應放大的雲端資料庫報告 | Microsoft Docs"
description: "如何設定水平資料分割的彈性查詢"
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
ms.openlocfilehash: 62b5bcd26aa1ed219fb38970916e0e8847ceb577
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="4e250-103">跨相應放大的雲端資料庫報告 (預覽)</span><span class="sxs-lookup"><span data-stu-id="4e250-103">Reporting across scaled-out cloud databases (preview)</span></span>
![跨分區查詢][1]

<span data-ttu-id="4e250-105">分區化資料庫跨相應放大的資料層發佈資料列。</span><span class="sxs-lookup"><span data-stu-id="4e250-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="4e250-106">所有參與的資料庫都有相同的結構描述，也稱為水平資料分割。</span><span class="sxs-lookup"><span data-stu-id="4e250-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="4e250-107">使用彈性查詢，您可以建立跨越分區化資料庫中所有資料庫的報告。</span><span class="sxs-lookup"><span data-stu-id="4e250-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="4e250-108">如需快速啟動，請參閱 [跨相應放大的雲端資料庫報告](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="4e250-109">如需非分區化資料庫，請參閱 [對不同結構描述的雲端資料庫執行查詢](sql-database-elastic-query-vertical-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4e250-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4e250-110">Prerequisites</span></span>
* <span data-ttu-id="4e250-111">使用彈性資料庫用戶端程式庫，建立分區對應。</span><span class="sxs-lookup"><span data-stu-id="4e250-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="4e250-112">請參閱 [分區對應管理](sql-database-elastic-scale-shard-map-management.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="4e250-113">或使用 [開始使用彈性資料庫工具](sql-database-elastic-scale-get-started.md)中的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e250-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="4e250-114">或者，請參閱 [轉換現有的資料庫以使用彈性資料庫工具](sql-database-elastic-convert-to-use-elastic-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="4e250-115">使用者必須擁有 ALTER ANY EXTERNAL DATA SOURCE 權限。</span><span class="sxs-lookup"><span data-stu-id="4e250-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="4e250-116">這個權限包含在 ALTER DATABASE 權限中。</span><span class="sxs-lookup"><span data-stu-id="4e250-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="4e250-117">需有 ALTER ANY EXTERNAL DATA SOURCE 權限，才能參考基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="4e250-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="4e250-118">概觀</span><span class="sxs-lookup"><span data-stu-id="4e250-118">Overview</span></span>
<span data-ttu-id="4e250-119">這些陳述式可在彈性查詢資料庫中建立分區化資料層的中繼資料表示法。</span><span class="sxs-lookup"><span data-stu-id="4e250-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="4e250-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="4e250-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="4e250-121">建立資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="4e250-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="4e250-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="4e250-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="4e250-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="4e250-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="4e250-124">1.1 建立資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="4e250-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="4e250-125">彈性查詢使用認證連接到遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="4e250-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="4e250-126">請確定 *"\<username\>"* 不含任何 *"@servername"* 後置詞。</span><span class="sxs-lookup"><span data-stu-id="4e250-126">Make sure that the *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="4e250-127">1.2 建立外部資料來源</span><span class="sxs-lookup"><span data-stu-id="4e250-127">1.2 Create external data sources</span></span>
<span data-ttu-id="4e250-128">語法：</span><span class="sxs-lookup"><span data-stu-id="4e250-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="4e250-129">範例</span><span class="sxs-lookup"><span data-stu-id="4e250-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="4e250-130">擷取目前的外部資料來源清單︰</span><span class="sxs-lookup"><span data-stu-id="4e250-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="4e250-131">外部資料來源會參考分區對應。</span><span class="sxs-lookup"><span data-stu-id="4e250-131">The external data source references your shard map.</span></span> <span data-ttu-id="4e250-132">彈性查詢會接著使用外部資料來源和基礎分區對應來列舉參與資料層的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4e250-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="4e250-133">在彈性查詢處理期間，使用相同的認證來讀取分區對應和存取分區上的資料。</span><span class="sxs-lookup"><span data-stu-id="4e250-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="4e250-134">1.3 建立外部資料表</span><span class="sxs-lookup"><span data-stu-id="4e250-134">1.3 Create external tables</span></span>
<span data-ttu-id="4e250-135">語法：</span><span class="sxs-lookup"><span data-stu-id="4e250-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="4e250-136">**範例**</span><span class="sxs-lookup"><span data-stu-id="4e250-136">**Example**</span></span>

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

<span data-ttu-id="4e250-137">從目前的資料庫擷取外部資料表清單：</span><span class="sxs-lookup"><span data-stu-id="4e250-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="4e250-138">捨棄外部資料表：</span><span class="sxs-lookup"><span data-stu-id="4e250-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="4e250-139">備註</span><span class="sxs-lookup"><span data-stu-id="4e250-139">Remarks</span></span>
<span data-ttu-id="4e250-140">DATA\_SOURCE 子句會定義用於外部資料表的外部資料來源 (分區對應)。</span><span class="sxs-lookup"><span data-stu-id="4e250-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="4e250-141">SCHEMA\_NAME 和 OBJECT\_NAME 子句會將外部資料表定義對應至不同結構描述中的資料表。</span><span class="sxs-lookup"><span data-stu-id="4e250-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="4e250-142">如果省略，即會假設遠端物件的結構描述為 "dbo" 並假設其名稱與所定義的外部資料表名稱相同。</span><span class="sxs-lookup"><span data-stu-id="4e250-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="4e250-143">如果您的遠端資料表名稱已存在於您要建立外部資料表的資料庫中，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="4e250-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="4e250-144">例如，您想要定義外部資料表以取得向外延展之資料層上目錄檢視或 DMV 的彙總檢視。</span><span class="sxs-lookup"><span data-stu-id="4e250-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="4e250-145">由於目錄檢視和 DMV 已經存在於本機，所以您無法將其名稱使用於外部資料表定義。</span><span class="sxs-lookup"><span data-stu-id="4e250-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="4e250-146">您需改為在 SCHEMA\_NAME 和/或 OBJECT\_NAME 子句中，使用不同的名稱以及使用目錄檢視名稱或 DMV 名稱。</span><span class="sxs-lookup"><span data-stu-id="4e250-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="4e250-147">(請參閱下面的範例)。</span><span class="sxs-lookup"><span data-stu-id="4e250-147">(See the example below.)</span></span> 

<span data-ttu-id="4e250-148">DISTRIBUTION 子句會指定用於此資料表的資料散發。</span><span class="sxs-lookup"><span data-stu-id="4e250-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="4e250-149">查詢處理器會利用 DISTRIBUTION 子句中提供的資訊來建置最有效率的查詢計劃。</span><span class="sxs-lookup"><span data-stu-id="4e250-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="4e250-150">**SHARDED** 表示跨資料庫水平分割資料。</span><span class="sxs-lookup"><span data-stu-id="4e250-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="4e250-151">用於資料散發的分割索引鍵是 **<sharding_column_name>** 參數。</span><span class="sxs-lookup"><span data-stu-id="4e250-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="4e250-152">**REPLICATED** 表示資料表的相同複本會存在於每個資料庫上。</span><span class="sxs-lookup"><span data-stu-id="4e250-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="4e250-153">您必須負責確保複本在所有資料庫上都相同。</span><span class="sxs-lookup"><span data-stu-id="4e250-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="4e250-154">**ROUND\_ROBIN** 表示使用應用程式相依的散發方法，以水平方式分割資料表。</span><span class="sxs-lookup"><span data-stu-id="4e250-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="4e250-155">**資料層參考**：外部資料表 DDL 指的是外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="4e250-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="4e250-156">外部資料來源會指定分區對應，以將找出資料層中的所有資料庫所需的資訊提供給外部資料表。</span><span class="sxs-lookup"><span data-stu-id="4e250-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="4e250-157">安全性考量</span><span class="sxs-lookup"><span data-stu-id="4e250-157">Security considerations</span></span>
<span data-ttu-id="4e250-158">可存取外部資料表的使用者可以在外部資料來源定義中所提供的認證下，自動取得基礎遠端資料表的存取權。</span><span class="sxs-lookup"><span data-stu-id="4e250-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="4e250-159">避免透過外部資料來源認證提高不想提高的權限。</span><span class="sxs-lookup"><span data-stu-id="4e250-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="4e250-160">對外部資料表使用「授與」或「撤銷」，就像它是一般的資料表一樣。</span><span class="sxs-lookup"><span data-stu-id="4e250-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="4e250-161">一旦您已定義外部資料來源和外部資料表，現在您可以對外部資料表使用完整的 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="4e250-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="4e250-162">範例︰查詢水平資料分割的資料庫</span><span class="sxs-lookup"><span data-stu-id="4e250-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="4e250-163">下列查詢在倉儲、訂單及訂單明細之間執行三方聯結，並使用數個彙總和選擇性篩選。</span><span class="sxs-lookup"><span data-stu-id="4e250-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="4e250-164">其假設 (1) 水平資料分割 (分區化) 以及 (2) 倉儲、訂單及訂單明細依倉儲識別碼資料行分區，而彈性查詢可以將聯結共置於分區上以及平行處理分區上成本較高的查詢部分。</span><span class="sxs-lookup"><span data-stu-id="4e250-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="4e250-165">用於遠端 T-SQL 執行的預存程序：sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="4e250-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="4e250-166">彈性查詢也會介紹可供直接存取分區的預存程序。</span><span class="sxs-lookup"><span data-stu-id="4e250-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="4e250-167">預存程序稱為 [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714)，可用來在遠端資料庫上執行遠端預存程序或 T-SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="4e250-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="4e250-168">它需要以下參數：</span><span class="sxs-lookup"><span data-stu-id="4e250-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="4e250-169">資料來源名稱 (nvarchar)：RDBMS 類型的外部資料來源名稱。</span><span class="sxs-lookup"><span data-stu-id="4e250-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="4e250-170">查詢 (nvarchar)：對每個分區執行的 T-SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="4e250-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="4e250-171">參數宣告 (nvarchar) - 選用：含有查詢參數 (如 sp_executesql) 中所用參數的資料類型定義的字串。</span><span class="sxs-lookup"><span data-stu-id="4e250-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="4e250-172">參數值清單 - 選用：以逗號分隔的參數值清單 (如 sp_executesql)。</span><span class="sxs-lookup"><span data-stu-id="4e250-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="4e250-173">sp\_execute\_remote 會使用叫用參數中提供的外部資料來源，在遠端資料庫上執行指定的 T-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="4e250-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="4e250-174">它會使用外部資料來源的認證連接 shardmap 管理員資料庫和遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="4e250-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="4e250-175">範例：</span><span class="sxs-lookup"><span data-stu-id="4e250-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="4e250-176">工具的連線能力</span><span class="sxs-lookup"><span data-stu-id="4e250-176">Connectivity for tools</span></span>
<span data-ttu-id="4e250-177">使用一般 SQL Server 連接字串，將您的應用程式、BI 和資料整合工具連接到包含外部資料表定義的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4e250-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="4e250-178">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="4e250-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="4e250-179">然後像任何其他連接到工具的 SQL Server 資料庫一樣，參考彈性查詢資料庫，並如同本機資料表一樣，從您的工具或應用程式使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="4e250-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="4e250-180">最佳作法</span><span class="sxs-lookup"><span data-stu-id="4e250-180">Best practices</span></span>
* <span data-ttu-id="4e250-181">請確定分區對應資料庫和所有分區都已透過 SQL DB 防火牆取得彈性查詢端點資料庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="4e250-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="4e250-182">驗證或強制執行外部資料表所定義的資料分佈。</span><span class="sxs-lookup"><span data-stu-id="4e250-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="4e250-183">如果您的實際資料分佈與資料表定義中指定的散發不同，您的查詢可能會產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="4e250-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="4e250-184">彈性查詢目前不會執行分區刪除，因為分區化索引鍵的述詞允許安全地排除處理某些分區。</span><span class="sxs-lookup"><span data-stu-id="4e250-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="4e250-185">彈性查詢最適合可在分區完成大部分運算的查詢。</span><span class="sxs-lookup"><span data-stu-id="4e250-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="4e250-186">使用可在分區上評估的選擇性篩選述詞，或在所有分區上以資料分割對齊方式來聯結資料分割索引鍵，通常可以獲得最佳查詢效能。</span><span class="sxs-lookup"><span data-stu-id="4e250-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="4e250-187">其他查詢模式可能需要從分區載入大量資料至前端節點，但效能可能不佳。</span><span class="sxs-lookup"><span data-stu-id="4e250-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e250-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e250-188">Next steps</span></span>

* <span data-ttu-id="4e250-189">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="4e250-190">若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="4e250-191">如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="4e250-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="4e250-192">如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="4e250-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="4e250-193">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="4e250-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
