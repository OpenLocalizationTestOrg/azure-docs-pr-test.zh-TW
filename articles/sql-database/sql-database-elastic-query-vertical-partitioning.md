---
title: "對不同結構描述的雲端資料庫執行查詢 | Microsoft Docs"
description: "如何透過垂直資料分割設定跨資料庫查詢"
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
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="d31bb-103">對不同結構描述的雲端資料庫執行查詢 (預覽)</span><span class="sxs-lookup"><span data-stu-id="d31bb-103">Query across cloud databases with different schemas (preview)</span></span>
![在不同資料庫中跨資料表查詢][1]

<span data-ttu-id="d31bb-105">垂直資料分割資料庫使用在不同資料庫的不同資料表集。</span><span class="sxs-lookup"><span data-stu-id="d31bb-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="d31bb-106">這表示不同資料庫的結構描述不同。</span><span class="sxs-lookup"><span data-stu-id="d31bb-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="d31bb-107">比方說，庫存的所有資料表都位於一個資料庫上，而所有會計相關資料表則位於另一個資料庫上。</span><span class="sxs-lookup"><span data-stu-id="d31bb-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d31bb-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d31bb-108">Prerequisites</span></span>
* <span data-ttu-id="d31bb-109">使用者必須擁有 ALTER ANY EXTERNAL DATA SOURCE 權限。</span><span class="sxs-lookup"><span data-stu-id="d31bb-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="d31bb-110">這個權限包含在 ALTER DATABASE 權限中。</span><span class="sxs-lookup"><span data-stu-id="d31bb-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="d31bb-111">需有 ALTER ANY EXTERNAL DATA SOURCE 權限，才能參考基礎資料來源。</span><span class="sxs-lookup"><span data-stu-id="d31bb-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="d31bb-112">概觀</span><span class="sxs-lookup"><span data-stu-id="d31bb-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="d31bb-113">與水平資料分割不同，這些 DDL 陳述式並不倚賴透過彈性資料庫用戶端程式庫來定義帶有分區對應的資料層。</span><span class="sxs-lookup"><span data-stu-id="d31bb-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="d31bb-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="d31bb-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="d31bb-115">建立資料庫範圍認證</span><span class="sxs-lookup"><span data-stu-id="d31bb-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="d31bb-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="d31bb-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="d31bb-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="d31bb-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="d31bb-118">建立資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="d31bb-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="d31bb-119">彈性查詢使用認證連接到遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="d31bb-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="d31bb-120">請確定 `<username>` 不包含任何 **"@servername"** 後置詞。</span><span class="sxs-lookup"><span data-stu-id="d31bb-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="d31bb-121">建立外部資料來源</span><span class="sxs-lookup"><span data-stu-id="d31bb-121">Create external data sources</span></span>
<span data-ttu-id="d31bb-122">語法：</span><span class="sxs-lookup"><span data-stu-id="d31bb-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="d31bb-123">TYPE 參數必須設定為 **RDBMS**。</span><span class="sxs-lookup"><span data-stu-id="d31bb-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="d31bb-124">範例</span><span class="sxs-lookup"><span data-stu-id="d31bb-124">Example</span></span>
<span data-ttu-id="d31bb-125">下列範例說明對外部資料來源使用 CREATE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d31bb-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="d31bb-126">若要擷取目前的外部資料來源清單︰</span><span class="sxs-lookup"><span data-stu-id="d31bb-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="d31bb-127">外部資料表</span><span class="sxs-lookup"><span data-stu-id="d31bb-127">External Tables</span></span>
<span data-ttu-id="d31bb-128">語法：</span><span class="sxs-lookup"><span data-stu-id="d31bb-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="d31bb-129">範例</span><span class="sxs-lookup"><span data-stu-id="d31bb-129">Example</span></span>
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

<span data-ttu-id="d31bb-130">下列範例顯示如何從目前資料庫擷取外部資料表清單：</span><span class="sxs-lookup"><span data-stu-id="d31bb-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="d31bb-131">備註</span><span class="sxs-lookup"><span data-stu-id="d31bb-131">Remarks</span></span>
<span data-ttu-id="d31bb-132">彈性的查詢會延伸現有的外部資料表語法來定義使用 RDBMS 類型外部資料來源的外部資料表。</span><span class="sxs-lookup"><span data-stu-id="d31bb-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="d31bb-133">垂直資料分割的外部資料表定義包含下列各方面：</span><span class="sxs-lookup"><span data-stu-id="d31bb-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="d31bb-134">**結構描述**：外部資料表 DDL 會定義您的查詢可以使用的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d31bb-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="d31bb-135">外部資料表定義中提供的結構描述必須符合實際資料儲存所在之遠端資料庫中資料表的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d31bb-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="d31bb-136">**遠端資料庫參考**：外部資料表 DDL 指的是外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="d31bb-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="d31bb-137">外部資料來源可指定邏輯伺服器名稱和實際資料表資料儲存所在之遠端資料庫的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="d31bb-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="d31bb-138">如上一節所述使用外部資料來源，建立外部資料表的語法如下：</span><span class="sxs-lookup"><span data-stu-id="d31bb-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="d31bb-139">DATA_SOURCE 子句會定義用於外部資料表的外部資料來源 (亦即垂直資料分割情形中的遠端資料庫)。</span><span class="sxs-lookup"><span data-stu-id="d31bb-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="d31bb-140">SCHEMA_NAME 和 OBJECT_NAME 子句提供的功能可將外部資料表定義分別對應至遠端資料庫上不同結構描述中的資料表，或對應至不同名稱的資料表。</span><span class="sxs-lookup"><span data-stu-id="d31bb-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="d31bb-141">不論是您想要為目錄檢視或遠端資料庫上的 DMV 定義外部資料表，還是在遠端資料表名稱在本機已被使用的任何其他情況下，這個方法都很實用。</span><span class="sxs-lookup"><span data-stu-id="d31bb-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="d31bb-142">下列 DDL 陳述式會從本機目錄卸除現有的外部資料表定義。</span><span class="sxs-lookup"><span data-stu-id="d31bb-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="d31bb-143">它不會影響遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="d31bb-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="d31bb-144">**CREATE/DROP EXTERNAL TABLE 的權限**：ALTER ANY EXTERNAL DATA SOURCE 權限對外部資料表 DDL 而言是必要的，而後者在參考基礎資料來源時也是必要的。</span><span class="sxs-lookup"><span data-stu-id="d31bb-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="d31bb-145">安全性考量</span><span class="sxs-lookup"><span data-stu-id="d31bb-145">Security considerations</span></span>
<span data-ttu-id="d31bb-146">可存取外部資料表的使用者可以在外部資料來源定義中所提供的認證下，自動取得基礎遠端資料表的存取權。</span><span class="sxs-lookup"><span data-stu-id="d31bb-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="d31bb-147">您應該仔細管理外部資料表的存取權，以避免透過外部資料來源的認證所造成的意外權限提升。</span><span class="sxs-lookup"><span data-stu-id="d31bb-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="d31bb-148">一般的 SQL 權限可用來授與或撤銷外部資料表的存取權，如同它是一般資料表那樣。</span><span class="sxs-lookup"><span data-stu-id="d31bb-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="d31bb-149">範例︰查詢垂直資料分割的資料庫</span><span class="sxs-lookup"><span data-stu-id="d31bb-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="d31bb-150">下列查詢會執行訂單和訂單明細的兩個本機資料表與客戶遠端資料表之間的三方聯結。</span><span class="sxs-lookup"><span data-stu-id="d31bb-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="d31bb-151">這是彈性查詢的參考資料使用案例的範例：</span><span class="sxs-lookup"><span data-stu-id="d31bb-151">This is an example of the reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="d31bb-152">用於遠端 T-SQL 執行的預存程序：sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="d31bb-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="d31bb-153">彈性查詢也會介紹可供直接存取分區的預存程序。</span><span class="sxs-lookup"><span data-stu-id="d31bb-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="d31bb-154">預存程序稱為 [sp\_execute\_remote](https://msdn.microsoft.com/library/mt703714)，可用來在遠端資料庫上執行遠端預存程序或 T-SQL 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d31bb-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="d31bb-155">它需要以下參數：</span><span class="sxs-lookup"><span data-stu-id="d31bb-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="d31bb-156">資料來源名稱 (nvarchar)：RDBMS 類型的外部資料來源名稱。</span><span class="sxs-lookup"><span data-stu-id="d31bb-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="d31bb-157">查詢 (nvarchar)：對每個分區執行的 T-SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d31bb-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="d31bb-158">參數宣告 (nvarchar) - 選用：含有查詢參數 (如 sp_executesql) 中所用參數的資料類型定義的字串。</span><span class="sxs-lookup"><span data-stu-id="d31bb-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="d31bb-159">參數值清單 - 選用：以逗號分隔的參數值清單 (如 sp_executesql)。</span><span class="sxs-lookup"><span data-stu-id="d31bb-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="d31bb-160">sp\_execute\_remote 會使用叫用參數中提供的外部資料來源，在遠端資料庫上執行指定的 T-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="d31bb-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="d31bb-161">它會使用外部資料來源的認證連接 shardmap 管理員資料庫和遠端資料庫。</span><span class="sxs-lookup"><span data-stu-id="d31bb-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="d31bb-162">範例：</span><span class="sxs-lookup"><span data-stu-id="d31bb-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="d31bb-163">工具的連線能力</span><span class="sxs-lookup"><span data-stu-id="d31bb-163">Connectivity for tools</span></span>
<span data-ttu-id="d31bb-164">您可以使用一般 SQL Server 連接字串，在啟用彈性查詢及定義外部資料表的 SQL DB 伺服器上，將 BI 和資料整合工具連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="d31bb-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="d31bb-165">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="d31bb-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="d31bb-166">然後參考彈性查詢資料庫和其外部資料表，就如同您會使用您的工具連接的任何其他 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d31bb-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="d31bb-167">最佳作法</span><span class="sxs-lookup"><span data-stu-id="d31bb-167">Best practices</span></span>
* <span data-ttu-id="d31bb-168">確保遠端資料庫已藉由在 Azure 服務的 SQL DB 防火牆組態中啟用其存取權，獲得彈性查詢端點資料庫的存取權。</span><span class="sxs-lookup"><span data-stu-id="d31bb-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="d31bb-169">也請確定外部資料來源定義中提供的認證可以成功登入遠端資料庫，而且具有存取遠端資料表的權限。</span><span class="sxs-lookup"><span data-stu-id="d31bb-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="d31bb-170">彈性查詢最適合可在遠端資料庫上完成大部分運算的查詢。</span><span class="sxs-lookup"><span data-stu-id="d31bb-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="d31bb-171">使用可在遠端資料庫上評估的選擇性篩選述詞，或可在遠端資料庫上完全執行的聯結，通常可以獲得最佳查詢效能。</span><span class="sxs-lookup"><span data-stu-id="d31bb-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="d31bb-172">其他查詢模式可能需要從遠端資料庫載入大量的資料，而且執行效能可能會很差。</span><span class="sxs-lookup"><span data-stu-id="d31bb-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d31bb-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d31bb-173">Next steps</span></span>

* <span data-ttu-id="d31bb-174">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d31bb-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="d31bb-175">若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。</span><span class="sxs-lookup"><span data-stu-id="d31bb-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="d31bb-176">如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="d31bb-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="d31bb-177">如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d31bb-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="d31bb-178">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="d31bb-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
