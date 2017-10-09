---
title: "雲端間 aaaQuery 資料庫具有不同的結構描述 |Microsoft 文件"
description: "如何 tooset 垂直分割區的跨資料庫查詢"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="c11b5-103">對不同結構描述的雲端資料庫執行查詢 (預覽)</span><span class="sxs-lookup"><span data-stu-id="c11b5-103">Query across cloud databases with different schemas (preview)</span></span>
![在不同資料庫中跨資料表查詢][1]

<span data-ttu-id="c11b5-105">垂直資料分割資料庫使用在不同資料庫的不同資料表集。</span><span class="sxs-lookup"><span data-stu-id="c11b5-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="c11b5-106">這表示該 hello 結構描述是在不同的資料庫不同。</span><span class="sxs-lookup"><span data-stu-id="c11b5-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="c11b5-107">比方說，庫存的所有資料表都位於一個資料庫上，而所有會計相關資料表則位於另一個資料庫上。</span><span class="sxs-lookup"><span data-stu-id="c11b5-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c11b5-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="c11b5-108">Prerequisites</span></span>
* <span data-ttu-id="c11b5-109">hello 使用者必須擁有 ALTER ANY EXTERNAL DATA SOURCE 權限。</span><span class="sxs-lookup"><span data-stu-id="c11b5-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="c11b5-110">此權限會包含 hello ALTER DATABASE 權限。</span><span class="sxs-lookup"><span data-stu-id="c11b5-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="c11b5-111">ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="c11b5-112">概觀</span><span class="sxs-lookup"><span data-stu-id="c11b5-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="c11b5-113">不同於與水平資料分割，這些 DDL 陳述式不相依於定義透過 hello 彈性資料庫用戶端程式庫的分區對應的資料層。</span><span class="sxs-lookup"><span data-stu-id="c11b5-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="c11b5-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="c11b5-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="c11b5-115">建立資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="c11b5-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="c11b5-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="c11b5-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="c11b5-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="c11b5-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="c11b5-118">建立資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="c11b5-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="c11b5-119">hello 認證會使用 hello 彈性查詢 tooconnect tooyour 遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="c11b5-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="c11b5-120">請確定該 hello`<username>`不包含任何**"@servername"**後置詞。</span><span class="sxs-lookup"><span data-stu-id="c11b5-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="c11b5-121">建立外部資料來源</span><span class="sxs-lookup"><span data-stu-id="c11b5-121">Create external data sources</span></span>
<span data-ttu-id="c11b5-122">語法：</span><span class="sxs-lookup"><span data-stu-id="c11b5-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="c11b5-123">hello 型別參數必須設定得**RDBMS**。</span><span class="sxs-lookup"><span data-stu-id="c11b5-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="c11b5-124">範例</span><span class="sxs-lookup"><span data-stu-id="c11b5-124">Example</span></span>
<span data-ttu-id="c11b5-125">hello 下列範例說明如何 hello 使用 hello CREATE 陳述式的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="c11b5-126">目前的外部資料來源 tooretrieve hello 清單：</span><span class="sxs-lookup"><span data-stu-id="c11b5-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="c11b5-127">外部資料表</span><span class="sxs-lookup"><span data-stu-id="c11b5-127">External Tables</span></span>
<span data-ttu-id="c11b5-128">語法：</span><span class="sxs-lookup"><span data-stu-id="c11b5-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="c11b5-129">範例</span><span class="sxs-lookup"><span data-stu-id="c11b5-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="c11b5-130">hello 下列範例顯示如何 tooretrieve hello hello 目前資料庫中的外部資料表的清單：</span><span class="sxs-lookup"><span data-stu-id="c11b5-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="c11b5-131">備註</span><span class="sxs-lookup"><span data-stu-id="c11b5-131">Remarks</span></span>
<span data-ttu-id="c11b5-132">彈性查詢擴充 hello 現有外部資料表語法 toodefine 外部資料表所使用的型別 RDBMS 外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="c11b5-133">垂直資料分割的外部資料表定義涵蓋 hello 下列層面：</span><span class="sxs-lookup"><span data-stu-id="c11b5-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="c11b5-134">**結構描述**: hello 外部資料表 DDL 會定義您的查詢可以使用的結構描述。</span><span class="sxs-lookup"><span data-stu-id="c11b5-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="c11b5-135">提供外部資料表定義中的 hello 結構描述必須 hello hello 實際資料的儲存位置的遠端資料庫中的 hello 資料表 toomatch hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="c11b5-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="c11b5-136">**遠端資料庫參考**: hello 外部資料表 DDL 參考 tooan 外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="c11b5-137">hello 外部資料來源指定 hello 邏輯伺服器名稱和 hello hello 實際的資料表資料的儲存位置的遠端資料庫的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="c11b5-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="c11b5-138">Hello 上一節中所述，請使用外部資料來源，hello 語法 toocreate 外部資料表如下所示：</span><span class="sxs-lookup"><span data-stu-id="c11b5-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="c11b5-139">hello DATA_SOURCE 子句會定義用於 hello 外部資料表的 hello 外部資料來源 （也就是 hello 遠端資料庫發生垂直資料分割）。</span><span class="sxs-lookup"><span data-stu-id="c11b5-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="c11b5-140">hello SCHEMA_NAME 和 OBJECT_NAME 子句 hello 能力 toomap hello 外部資料表定義 tooa 資料表不同的結構描述中 hello 遠端資料庫或使用不同的名稱，tooa 資料表上分別提供。</span><span class="sxs-lookup"><span data-stu-id="c11b5-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="c11b5-141">這是如果您想 toodefine 外部資料表 tooa 目錄檢視或 DMV 遠端的資料庫-或任何其他地方 hello 遠端資料表名稱已被使用在本機的情況下很有用。</span><span class="sxs-lookup"><span data-stu-id="c11b5-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="c11b5-142">hello 下列 DDL 陳述式從卸除現有的外部資料表定義 hello 本機類別目錄。</span><span class="sxs-lookup"><span data-stu-id="c11b5-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="c11b5-143">它不會影響 hello 遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="c11b5-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="c11b5-144">**CREATE/DROP 外部資料表的權限**: ALTER ANY EXTERNAL DATA SOURCE 權限所需的外部資料表 DDL 這也是需要 toorefer toohello 基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="c11b5-145">安全性考量</span><span class="sxs-lookup"><span data-stu-id="c11b5-145">Security considerations</span></span>
<span data-ttu-id="c11b5-146">使用者具有存取 toohello 外部資料表會自動存取 toohello 基礎遠端的資料表在 hello hello 外部資料來源定義中提供的認證。</span><span class="sxs-lookup"><span data-stu-id="c11b5-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="c11b5-147">您應謹慎管理順序 tooavoid 討厭的權限提高的權限透過 hello hello 外部資料來源的認證存取 toohello 外部資料表。</span><span class="sxs-lookup"><span data-stu-id="c11b5-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="c11b5-148">規則的 SQL 權限可以在使用的 tooGRANT 或 REVOKE access tooan 外部資料表就如同一般資料表。</span><span class="sxs-lookup"><span data-stu-id="c11b5-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="c11b5-149">範例︰查詢垂直資料分割的資料庫</span><span class="sxs-lookup"><span data-stu-id="c11b5-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="c11b5-150">hello 下列查詢會執行三向聯結 hello 兩個區域的資料表訂單和訂單產品線之間 hello 遠端資料表的客戶。</span><span class="sxs-lookup"><span data-stu-id="c11b5-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="c11b5-151">這是 hello 參考資料彈性查詢的使用案例的範例：</span><span class="sxs-lookup"><span data-stu-id="c11b5-151">This is an example of hello reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="c11b5-152">用於遠端 T-SQL 執行的預存程序：sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="c11b5-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="c11b5-153">彈性查詢也會介紹可直接存取 toohello 分區的預存程序。</span><span class="sxs-lookup"><span data-stu-id="c11b5-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="c11b5-154">hello 預存程序稱為[sp\_執行\_遠端](https://msdn.microsoft.com/library/mt703714)而且可以是使用的 tooexecute 遠端預存程序或 hello 遠端資料庫上的 T-SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c11b5-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="c11b5-155">它會採用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="c11b5-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="c11b5-156">資料來源名稱 (nvarchar): hello hello 類型 RDBMS 外部資料來源名稱。</span><span class="sxs-lookup"><span data-stu-id="c11b5-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="c11b5-157">查詢 (nvarchar): hello T-SQL 查詢 toobe 在每個分區上執行。</span><span class="sxs-lookup"><span data-stu-id="c11b5-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="c11b5-158">參數宣告 (nvarchar)-選擇性： hello 查詢參數 （例如 sp_executesql) 中使用的 hello 參數的資料型別定義的字串。</span><span class="sxs-lookup"><span data-stu-id="c11b5-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="c11b5-159">參數值清單 - 選用：以逗號分隔的參數值清單 (如 sp_executesql)。</span><span class="sxs-lookup"><span data-stu-id="c11b5-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="c11b5-160">hello sp\_執行\_遠端使用 hello hello 引動過程參數 tooexecute hello hello 遠端資料庫上給定 T-SQL 陳述式中提供的外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="c11b5-161">它會使用 hello hello 外部資料來源 tooconnect toohello shardmap manager 資料庫和 hello 遠端資料庫的認證。</span><span class="sxs-lookup"><span data-stu-id="c11b5-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="c11b5-162">範例：</span><span class="sxs-lookup"><span data-stu-id="c11b5-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="c11b5-163">工具的連線能力</span><span class="sxs-lookup"><span data-stu-id="c11b5-163">Connectivity for tools</span></span>
<span data-ttu-id="c11b5-164">您可以使用一般 SQL Server 連接字串 tooconnect 您 BI 和資料整合工具 toodatabases，已啟用的彈性查詢和定義的外部資料表的 hello SQL 資料庫伺服器上。</span><span class="sxs-lookup"><span data-stu-id="c11b5-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="c11b5-165">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="c11b5-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="c11b5-166">然後，請參閱 toohello 彈性查詢資料庫與外部資料表就像其他任何 SQL Server 資料庫連線 toowith 工具一樣。</span><span class="sxs-lookup"><span data-stu-id="c11b5-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="c11b5-167">最佳作法</span><span class="sxs-lookup"><span data-stu-id="c11b5-167">Best practices</span></span>
* <span data-ttu-id="c11b5-168">請確定該 hello 彈性查詢端點的資料庫具有存取 toohello 遠端資料庫，進而存取 Azure 服務在 SQL 資料庫的防火牆設定。</span><span class="sxs-lookup"><span data-stu-id="c11b5-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="c11b5-169">提供在 hello 外部資料來源定義可以成功登入 hello 遠端資料庫，並有 hello 權限 tooaccess hello 遠端資料表，也請確定該 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="c11b5-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="c11b5-170">彈性查詢最適合查詢其中完成大部分的 hello 計算 hello 遠端資料庫上。</span><span class="sxs-lookup"><span data-stu-id="c11b5-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="c11b5-171">通常，您會收到包含選擇性的篩選器述詞可以在 hello 遠端資料庫或可執行 hello 遠端資料庫上的完全聯結評估 hello 最佳查詢效能。</span><span class="sxs-lookup"><span data-stu-id="c11b5-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="c11b5-172">其他的查詢模式可能需要 tooload 大量 hello 遠端資料庫中的資料，以及執行效能很差。</span><span class="sxs-lookup"><span data-stu-id="c11b5-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c11b5-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c11b5-173">Next steps</span></span>

* <span data-ttu-id="c11b5-174">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c11b5-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c11b5-175">若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。</span><span class="sxs-lookup"><span data-stu-id="c11b5-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="c11b5-176">如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c11b5-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="c11b5-177">如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c11b5-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c11b5-178">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="c11b5-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
