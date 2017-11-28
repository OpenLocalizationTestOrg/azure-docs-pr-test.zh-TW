---
title: "跨相應放大雲端資料庫報告 (水平分割) | Microsoft Docs"
description: "如何使用跨資料庫的資料庫查詢"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="f5df1-103">跨相應放大雲端資料庫報告 (預覽)</span><span class="sxs-lookup"><span data-stu-id="f5df1-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="f5df1-104">您可以使用 [彈性查詢](sql-database-elastic-query-overview.md)，從單一連接點的多個 Azure SQL Database 建立報告。</span><span class="sxs-lookup"><span data-stu-id="f5df1-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="f5df1-105">資料庫必須水平分割 (也稱為「分區化」)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="f5df1-106">如果您有現有的資料庫，請參閱 [將現有的資料庫移轉到相應放大的資料庫](sql-database-elastic-convert-to-use-elastic-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="f5df1-107">若要了解查詢所需的 SQL 物件，請參閱 [跨水平分割資料庫查詢](sql-database-elastic-query-horizontal-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5df1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f5df1-108">Prerequisites</span></span>
<span data-ttu-id="f5df1-109">下載並執行 [彈性資料庫工具範例入門](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="f5df1-110">使用範例應用程式建立分區對應管理員</span><span class="sxs-lookup"><span data-stu-id="f5df1-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="f5df1-111">在這裡，您將建立分區對應管理員以及數個分區，接著插入資料至分區。</span><span class="sxs-lookup"><span data-stu-id="f5df1-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="f5df1-112">若您的分區設定中已有分區資料，則可以略過下列步驟並移至下一節。</span><span class="sxs-lookup"><span data-stu-id="f5df1-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="f5df1-113">建置並執行 **彈性資料庫工具入門** 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="f5df1-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="f5df1-114">遵循步驟，直到[下載及執行範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)小節的步驟 7。</span><span class="sxs-lookup"><span data-stu-id="f5df1-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="f5df1-115">在步驟 7 結束時，您會看到下列的命令提示字元：</span><span class="sxs-lookup"><span data-stu-id="f5df1-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![命令提示字元][1]
2. <span data-ttu-id="f5df1-117">在命令視窗中，輸入 "1"，然後按 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="f5df1-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="f5df1-118">這會建立分區對應管理員，並加入兩個分區到伺服器。</span><span class="sxs-lookup"><span data-stu-id="f5df1-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="f5df1-119">然後輸入 "3"，然後按 **Enter**；重複此動作四次。</span><span class="sxs-lookup"><span data-stu-id="f5df1-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="f5df1-120">這會在您的分區中插入範例資料列。</span><span class="sxs-lookup"><span data-stu-id="f5df1-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="f5df1-121">[Azure 入口網站](https://portal.azure.com)應該會在您的伺服器中顯示三個新的資料庫：</span><span class="sxs-lookup"><span data-stu-id="f5df1-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio 確認][2]

   <span data-ttu-id="f5df1-123">目前，跨資料庫查詢是透過彈性資料庫用戶端程式庫支援。</span><span class="sxs-lookup"><span data-stu-id="f5df1-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="f5df1-124">例如，在命令視窗中使用第 4 個選項。</span><span class="sxs-lookup"><span data-stu-id="f5df1-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="f5df1-125">來自多個分區查詢的結果永遠是所有分區的結果的 **全部聯集** 。</span><span class="sxs-lookup"><span data-stu-id="f5df1-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="f5df1-126">在下一節中，我們會建立支援更豐富的跨分區資料查詢的範例資料庫端點。</span><span class="sxs-lookup"><span data-stu-id="f5df1-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="f5df1-127">建立彈性的查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="f5df1-127">Create an elastic query database</span></span>
1. <span data-ttu-id="f5df1-128">開啟 [Azure 入口網站](https://portal.azure.com)並登入。</span><span class="sxs-lookup"><span data-stu-id="f5df1-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="f5df1-129">在與分區安裝程式相同的伺服器中建立新的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f5df1-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="f5df1-130">將資料庫命名為 "ElasticDBQuery"。</span><span class="sxs-lookup"><span data-stu-id="f5df1-130">Name the database "ElasticDBQuery."</span></span>

    ![Azure 入口網站和定價層][3]

    > [!NOTE]
    > <span data-ttu-id="f5df1-132">您可以使用現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5df1-132">you can use an existing database.</span></span> <span data-ttu-id="f5df1-133">如果您可以這樣做，它不得是您想要對其執行查詢的其中一個分區。</span><span class="sxs-lookup"><span data-stu-id="f5df1-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="f5df1-134">此資料庫將用於為彈性資料庫查詢建立中繼資料物件。</span><span class="sxs-lookup"><span data-stu-id="f5df1-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="f5df1-135">建立資料庫物件</span><span class="sxs-lookup"><span data-stu-id="f5df1-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="f5df1-136">資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="f5df1-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="f5df1-137">這些是用來連接到分區對應管理員和分區：</span><span class="sxs-lookup"><span data-stu-id="f5df1-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="f5df1-138">在 Visual Studio 中開啟 SQL Server Management Studio 或 SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="f5df1-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="f5df1-139">連接至 ElasticDBQuery 資料庫，並執行下列 T-SQL 命令：</span><span class="sxs-lookup"><span data-stu-id="f5df1-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="f5df1-140">"username" 和 "password" 應該與[彈性資料庫工具入門](sql-database-elastic-scale-get-started.md)中[下載及執行範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)的步驟 6 中所使用的登入資訊相同。</span><span class="sxs-lookup"><span data-stu-id="f5df1-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="f5df1-141">外部資料來源</span><span class="sxs-lookup"><span data-stu-id="f5df1-141">External data sources</span></span>
<span data-ttu-id="f5df1-142">若要建立外部資料來源，請在 ElasticDBQuery 資料庫上執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f5df1-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="f5df1-143">如果您使用彈性資料庫工具範例來建立分區對應和分區對應管理員，"CustomerIDShardMap" 會是分區對應的名稱。</span><span class="sxs-lookup"><span data-stu-id="f5df1-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="f5df1-144">不過，如果您為此範例使用您的自訂安裝程式，它應該是您在應用程式中選擇的分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="f5df1-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="f5df1-145">外部資料表</span><span class="sxs-lookup"><span data-stu-id="f5df1-145">External tables</span></span>
<span data-ttu-id="f5df1-146">在 ElasticDBQuery 資料庫上執行下列命令，建立符合分區上的客戶資料表外部資料表：</span><span class="sxs-lookup"><span data-stu-id="f5df1-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="f5df1-147">執行範例彈性資料庫 T-SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="f5df1-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="f5df1-148">一旦您已定義外部資料來源和外部資料表，現在您可以對外部資料表使用完整的 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="f5df1-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="f5df1-149">在 ElasticDBQuery 資料庫上執行此查詢：</span><span class="sxs-lookup"><span data-stu-id="f5df1-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="f5df1-150">您會注意到查詢會從所有分區彙總結果，並提供下列輸出：</span><span class="sxs-lookup"><span data-stu-id="f5df1-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![輸出詳細資料][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="f5df1-152">匯入彈性資料庫查詢結果到 Excel</span><span class="sxs-lookup"><span data-stu-id="f5df1-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="f5df1-153">您可以從查詢的結果匯入到 Excel 檔案。</span><span class="sxs-lookup"><span data-stu-id="f5df1-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="f5df1-154">啟動 Excel 2013。</span><span class="sxs-lookup"><span data-stu-id="f5df1-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="f5df1-155">瀏覽至 [ **資料** ] 功能區。</span><span class="sxs-lookup"><span data-stu-id="f5df1-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="f5df1-156">按一下 [從其他來源]，然後按一下 [從 SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="f5df1-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![從其他來源的 Excel 匯入][5]
4. <span data-ttu-id="f5df1-158">在 [ **資料連線精靈** ] 中，輸入伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="f5df1-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="f5df1-159">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="f5df1-159">Then click **Next**.</span></span>
5. <span data-ttu-id="f5df1-160">在對話方塊 [選取包含您想要的資料的資料庫] 中，選取 **ElasticDBQuery** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5df1-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="f5df1-161">在清單檢視中選取 [客戶] 資料表，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f5df1-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="f5df1-162">然後按一下 [ **完成**]。</span><span class="sxs-lookup"><span data-stu-id="f5df1-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="f5df1-163">在 [匯入資料] 表單中，於 [選取您要在活頁簿中檢視此資料的方式] 下，選取 [資料表]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f5df1-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="f5df1-164">儲存在不同分區中、來自 [客戶]  資料表的所有資料列會填入 Excel 工作表。</span><span class="sxs-lookup"><span data-stu-id="f5df1-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="f5df1-165">您現在可以使用 Excel 強大的資料視覺化功能。</span><span class="sxs-lookup"><span data-stu-id="f5df1-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="f5df1-166">您可以使用具備您的伺服器名稱、資料庫名稱和認證的連接字串來連接您的 BI 和資料整合工具至彈性查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="f5df1-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="f5df1-167">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="f5df1-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="f5df1-168">您可以參考彈性查詢資料庫和外部資料表，就如同您會使用您的工具連接的任何其他 SQL Server 資料庫和 SQL Server 資料表。</span><span class="sxs-lookup"><span data-stu-id="f5df1-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="f5df1-169">成本</span><span class="sxs-lookup"><span data-stu-id="f5df1-169">Cost</span></span>
<span data-ttu-id="f5df1-170">使用彈性資料庫查詢功能不另行收費。</span><span class="sxs-lookup"><span data-stu-id="f5df1-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="f5df1-171">如需價格資訊，請參閱 [SQL Database 價格詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5df1-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5df1-172">Next steps</span></span>

* <span data-ttu-id="f5df1-173">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="f5df1-174">若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="f5df1-175">如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="f5df1-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="f5df1-176">如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="f5df1-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="f5df1-177">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="f5df1-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
