---
title: "（水平資料分割） 的向外延展雲端資料庫之間的 aaaReport |Microsoft 文件"
description: "toouse 如何跨資料庫的資料庫查詢"
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
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="09f2c-103">跨相應放大雲端資料庫報告 (預覽)</span><span class="sxs-lookup"><span data-stu-id="09f2c-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="09f2c-104">您可以使用 [彈性查詢](sql-database-elastic-query-overview.md)，從單一連接點的多個 Azure SQL Database 建立報告。</span><span class="sxs-lookup"><span data-stu-id="09f2c-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="09f2c-105">hello 資料庫必須進行水平資料分割 （也稱為 「 分區 」）。</span><span class="sxs-lookup"><span data-stu-id="09f2c-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="09f2c-106">如果您有現有的資料庫，請參閱[移轉現有的資料庫 tooscaled 外資料庫](sql-database-elastic-convert-to-use-elastic-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="09f2c-107">需要 tooquery 的 toounderstand hello SQL 物件，請參閱[跨水平資料分割的資料庫查詢](sql-database-elastic-query-horizontal-partitioning.md)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09f2c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="09f2c-108">Prerequisites</span></span>
<span data-ttu-id="09f2c-109">下載並執行 hello[入門彈性資料庫工具範例](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="09f2c-110">建立分區對應管理員使用 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="09f2c-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="09f2c-111">這裡您將建立的分區對應管理員以及數個分區，後面接著插入資料至 hello 分區。</span><span class="sxs-lookup"><span data-stu-id="09f2c-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="09f2c-112">如果您遇到 tooalready 中有分區安裝過程中的使用分區化資料，您可以略過下列步驟的 hello 和移動 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="09f2c-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="09f2c-113">建置並執行 hello**彈性資料庫工具使用者入門**範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="09f2c-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="09f2c-114">步驟 7 hello > 一節中的 hello 步驟[下載並執行 hello 範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="09f2c-115">在步驟 7 hello 最後，您會看到下列命令提示字元中的 hello:</span><span class="sxs-lookup"><span data-stu-id="09f2c-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![命令提示字元][1]
2. <span data-ttu-id="09f2c-117">在 hello 命令視窗中，輸入"1"，然後按**Enter**。</span><span class="sxs-lookup"><span data-stu-id="09f2c-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="09f2c-118">這會建立 hello 分區對應管理員，並將這兩個分區 toohello 伺服器時。</span><span class="sxs-lookup"><span data-stu-id="09f2c-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="09f2c-119">然後輸入"3"，然後按**Enter**; 四次重複 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="09f2c-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="09f2c-120">這會在您的分區中插入範例資料列。</span><span class="sxs-lookup"><span data-stu-id="09f2c-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="09f2c-121">hello [Azure 入口網站](https://portal.azure.com)中您的伺服器應該會顯示三個新的資料庫：</span><span class="sxs-lookup"><span data-stu-id="09f2c-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio 確認][2]

   <span data-ttu-id="09f2c-123">此時，透過 hello 彈性資料庫用戶端程式庫支援跨資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="09f2c-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="09f2c-124">例如，使用選項 4 hello 命令視窗中。</span><span class="sxs-lookup"><span data-stu-id="09f2c-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="09f2c-125">hello 查詢結果的多個分區都**UNION ALL**的所有分區 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="09f2c-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="09f2c-126">Hello 下一節，我們會建立範例資料庫支援之端點的跨分區的 hello 資料更豐富查詢。</span><span class="sxs-lookup"><span data-stu-id="09f2c-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="09f2c-127">建立彈性的查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="09f2c-127">Create an elastic query database</span></span>
1. <span data-ttu-id="09f2c-128">開啟 hello [Azure 入口網站](https://portal.azure.com)並登入。</span><span class="sxs-lookup"><span data-stu-id="09f2c-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="09f2c-129">在 hello 中建立新的 Azure SQL database 分區安裝相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="09f2c-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="09f2c-130">名稱 hello 資料庫 」 ElasticDBQuery。 」</span><span class="sxs-lookup"><span data-stu-id="09f2c-130">Name hello database "ElasticDBQuery."</span></span>

    ![Azure 入口網站和定價層][3]

    > [!NOTE]
    > <span data-ttu-id="09f2c-132">您可以使用現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="09f2c-132">you can use an existing database.</span></span> <span data-ttu-id="09f2c-133">如果您可以這樣做，它不得為您想要 tooexecute hello 分區的其中一個查詢。</span><span class="sxs-lookup"><span data-stu-id="09f2c-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="09f2c-134">這個資料庫會用於建立 hello 彈性資料庫查詢的中繼資料物件。</span><span class="sxs-lookup"><span data-stu-id="09f2c-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="09f2c-135">建立資料庫物件</span><span class="sxs-lookup"><span data-stu-id="09f2c-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="09f2c-136">資料庫範圍的主要金鑰和認證</span><span class="sxs-lookup"><span data-stu-id="09f2c-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="09f2c-137">這些是使用的 tooconnect toohello 分區對應管理員與 hello 分區：</span><span class="sxs-lookup"><span data-stu-id="09f2c-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="09f2c-138">在 Visual Studio 中開啟 SQL Server Management Studio 或 SQL Server Data Tools</span><span class="sxs-lookup"><span data-stu-id="09f2c-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="09f2c-139">連接 tooElasticDBQuery 資料庫，然後執行下列 T-SQL 命令 hello:</span><span class="sxs-lookup"><span data-stu-id="09f2c-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="09f2c-140">「 使用者名稱 」 和 「 密碼 」 應該是 hello 相同的步驟 6 中所用的登入資訊為[下載並執行 hello 範例應用程式](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app)中[彈性資料庫工具使用者入門](sql-database-elastic-scale-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="09f2c-141">外部資料來源</span><span class="sxs-lookup"><span data-stu-id="09f2c-141">External data sources</span></span>
<span data-ttu-id="09f2c-142">toocreate 外部資料來源，執行下列命令 hello ElasticDBQuery 資料庫上的 hello:</span><span class="sxs-lookup"><span data-stu-id="09f2c-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="09f2c-143">「 CustomerIDShardMap 」 是 hello 分區對應，hello 名稱，如果您建立 hello 分區對應和分區對應管理員使用 hello 彈性資料庫工具範例。</span><span class="sxs-lookup"><span data-stu-id="09f2c-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="09f2c-144">不過，如果您使用您自訂的設定，此範例，它應該是您選擇在您的應用程式中的 hello 分區對應名稱。</span><span class="sxs-lookup"><span data-stu-id="09f2c-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="09f2c-145">外部資料表</span><span class="sxs-lookup"><span data-stu-id="09f2c-145">External tables</span></span>
<span data-ttu-id="09f2c-146">建立藉由執行下列命令 ElasticDBQuery 資料庫上的 hello 符合上 hello 分區 hello Customers 資料表的外部資料表：</span><span class="sxs-lookup"><span data-stu-id="09f2c-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="09f2c-147">執行範例彈性資料庫 T-SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="09f2c-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="09f2c-148">一旦您已定義外部資料來源和外部資料表，現在您可以對外部資料表使用完整的 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="09f2c-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="09f2c-149">Hello ElasticDBQuery 資料庫上執行下列查詢：</span><span class="sxs-lookup"><span data-stu-id="09f2c-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="09f2c-150">您會發現該 hello 查詢從所有 hello 分區彙總結果，並提供 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="09f2c-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![輸出詳細資料][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="09f2c-152">匯入彈性資料庫查詢結果 tooExcel</span><span class="sxs-lookup"><span data-stu-id="09f2c-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="09f2c-153">您可以匯入 hello 結果的查詢 tooan Excel 檔案。</span><span class="sxs-lookup"><span data-stu-id="09f2c-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="09f2c-154">啟動 Excel 2013。</span><span class="sxs-lookup"><span data-stu-id="09f2c-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="09f2c-155">瀏覽 toohello**資料**功能區。</span><span class="sxs-lookup"><span data-stu-id="09f2c-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="09f2c-156">按一下 [從其他來源]，然後按一下 [從 SQL Server]。</span><span class="sxs-lookup"><span data-stu-id="09f2c-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![從其他來源的 Excel 匯入][5]
4. <span data-ttu-id="09f2c-158">在 hello**資料連線精靈**輸入 hello 伺服器名稱和登入認證。</span><span class="sxs-lookup"><span data-stu-id="09f2c-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="09f2c-159">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="09f2c-159">Then click **Next**.</span></span>
5. <span data-ttu-id="09f2c-160">在 hello 對話方塊**選取 hello 資料庫包含您想要的 hello 資料**，選取 hello **ElasticDBQuery**資料庫。</span><span class="sxs-lookup"><span data-stu-id="09f2c-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="09f2c-161">選取 hello**客戶**hello 清單檢視中資料表，並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="09f2c-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="09f2c-162">然後按一下 [ **完成**]。</span><span class="sxs-lookup"><span data-stu-id="09f2c-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="09f2c-163">在 hello**匯入資料**底下形成**選取您要如何 tooview 這項資料在活頁簿中**，選取**資料表**按一下**[確定]**。</span><span class="sxs-lookup"><span data-stu-id="09f2c-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="09f2c-164">所有 hello 中的資料列**客戶**儲存在不同的分區中的資料表填入 hello Excel 工作表。</span><span class="sxs-lookup"><span data-stu-id="09f2c-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="09f2c-165">您現在可以使用 Excel 強大的資料視覺化功能。</span><span class="sxs-lookup"><span data-stu-id="09f2c-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="09f2c-166">您可以使用與您的伺服器名稱、 資料庫名稱的 hello 連接字串和認證 tooconnect BI 和資料整合工具 toohello 彈性查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="09f2c-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="09f2c-167">請確定 SQL Server 可支援做為您的工具的資料來源。</span><span class="sxs-lookup"><span data-stu-id="09f2c-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="09f2c-168">您可以參考 toohello 彈性查詢資料庫，就像任何其他 SQL Server 資料庫的外部資料表和連線 toowith 工具的 SQL Server 資料表。</span><span class="sxs-lookup"><span data-stu-id="09f2c-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="09f2c-169">成本</span><span class="sxs-lookup"><span data-stu-id="09f2c-169">Cost</span></span>
<span data-ttu-id="09f2c-170">沒有另收費用使用 hello 彈性資料庫查詢功能。</span><span class="sxs-lookup"><span data-stu-id="09f2c-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="09f2c-171">如需價格資訊，請參閱 [SQL Database 價格詳細資料](https://azure.microsoft.com/pricing/details/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09f2c-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09f2c-172">Next steps</span></span>

* <span data-ttu-id="09f2c-173">如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="09f2c-174">若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="09f2c-175">如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="09f2c-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="09f2c-176">如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="09f2c-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="09f2c-177">如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。</span><span class="sxs-lookup"><span data-stu-id="09f2c-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
