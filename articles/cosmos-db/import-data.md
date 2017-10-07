---
title: "Azure Cosmos DB 的 aaaDatabase 移轉工具 |Microsoft 文件"
description: "了解 toouse hello 開啟來源 Azure Cosmos DB 的資料移轉工具 tooimport 資料 tooAzure Cosmos DB 從各種來源納入 MongoDB、 SQL Server、 資料表儲存體、 Amazon DynamoDB、 CSV 和 JSON 檔案的方式。 CSV tooJSON 轉換。"
keywords: "csv toojson，資料庫移轉工具，將轉換 csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="625e0-105">如何針對 Azure Cosmos DB tooimport 資料 hello DocumentDB API 嗎？</span><span class="sxs-lookup"><span data-stu-id="625e0-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="625e0-106">本教學課程提供說明如何使用 hello Azure Cosmos DB: DocumentDB API 資料移轉工具，可以從各種來源，包括 JSON 檔案匯入資料 CSV 檔案、 SQL、 MongoDB、 Azure 資料表儲存體，Amazon DynamoDB 和 Azure Cosmos DB DocumentDB集合中的 API 集合使用 Azure Cosmos DB 與 hello DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="625e0-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="625e0-107">hello DocumentDB API，單一資料分割集合 tooa 多個資料分割集合移轉時，可以也使用 hello 資料移轉工具。</span><span class="sxs-lookup"><span data-stu-id="625e0-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="625e0-108">當匯入資料到 Azure DB Cosmos 使用 hello DocumentDB API 時，只適用於 hello 資料移轉工具。</span><span class="sxs-lookup"><span data-stu-id="625e0-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="625e0-109">在此階段不支援匯入適用於 hello 表格 API 或 Graph API 的資料。</span><span class="sxs-lookup"><span data-stu-id="625e0-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="625e0-110">tooimport hello MongoDB API 搭配使用的資料，請參閱[Azure Cosmos DB: toomigrate 資料如何 hello MongoDB API？](mongodb-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="625e0-111">本教學課程涵蓋 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="625e0-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="625e0-112">安裝 hello 資料移轉工具</span><span class="sxs-lookup"><span data-stu-id="625e0-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="625e0-113">從不同的資料來源匯入資料</span><span class="sxs-lookup"><span data-stu-id="625e0-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="625e0-114">從 Azure Cosmos DB tooJSON 匯出</span><span class="sxs-lookup"><span data-stu-id="625e0-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="625e0-115"><a id="Prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="625e0-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="625e0-116">之前遵循這篇文章中的 hello 指示，請確定您擁有 hello 安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="625e0-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="625e0-117">[Microsoft.NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="625e0-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="625e0-118"><a id="Overviewl"></a>Hello 資料移轉工具的概觀</span><span class="sxs-lookup"><span data-stu-id="625e0-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="625e0-119">hello 資料移轉工具是開放原始碼解決方案從各種不同的來源，包括匯入資料 tooAzure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="625e0-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="625e0-120">JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-120">JSON files</span></span>
* <span data-ttu-id="625e0-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="625e0-121">MongoDB</span></span>
* <span data-ttu-id="625e0-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="625e0-122">SQL Server</span></span>
* <span data-ttu-id="625e0-123">CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-123">CSV files</span></span>
* <span data-ttu-id="625e0-124">Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="625e0-124">Azure Table storage</span></span>
* <span data-ttu-id="625e0-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="625e0-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="625e0-126">HBase</span><span class="sxs-lookup"><span data-stu-id="625e0-126">HBase</span></span>
* <span data-ttu-id="625e0-127">Azure Cosmos DB 集合</span><span class="sxs-lookup"><span data-stu-id="625e0-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="625e0-128">雖然 hello 匯入工具包含圖形化使用者介面 (dtui.exe)，它可以也衍生自 hello 命令列 (dt.exe)。</span><span class="sxs-lookup"><span data-stu-id="625e0-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="625e0-129">事實上，設定透過 hello UI 匯入之後沒有選項 toooutput hello 相關聯的命令。</span><span class="sxs-lookup"><span data-stu-id="625e0-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="625e0-130">表格式來源資料 (例如 SQL Server 或 CSV 檔案) 可以進行轉換，以致可以在匯入期間建立階層式關聯性 (子文件)。</span><span class="sxs-lookup"><span data-stu-id="625e0-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="625e0-131">繼續閱讀更多有關來源選項，每個來源的範例命令列 tooimport toolearn、 目標選項和檢視結果匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="625e0-132"><a id="Install"></a>安裝 hello 資料移轉工具</span><span class="sxs-lookup"><span data-stu-id="625e0-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="625e0-133">hello 移轉工具的原始程式碼可在 GitHub 上[這個儲存機制](https://github.com/azure/azure-documentdb-datamigrationtool)而且編譯的版本都可從[Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)。</span><span class="sxs-lookup"><span data-stu-id="625e0-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="625e0-134">您可能會編譯 hello 方案或只是下載及擷取您所選擇的 hello 編譯的版本 tooa 目錄。</span><span class="sxs-lookup"><span data-stu-id="625e0-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="625e0-135">然後執行：</span><span class="sxs-lookup"><span data-stu-id="625e0-135">Then run either:</span></span>

* <span data-ttu-id="625e0-136">**Dtui.exe**: hello 工具的圖形化介面版本</span><span class="sxs-lookup"><span data-stu-id="625e0-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="625e0-137">**Dt.exe**: hello 工具命令列版本</span><span class="sxs-lookup"><span data-stu-id="625e0-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="625e0-138">匯入資料</span><span class="sxs-lookup"><span data-stu-id="625e0-138">Import data</span></span>

<span data-ttu-id="625e0-139">一旦您已安裝 hello 工具，就是時間 tooimport 您的資料。</span><span class="sxs-lookup"><span data-stu-id="625e0-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="625e0-140">何種類型的資料是否要 tooimport？</span><span class="sxs-lookup"><span data-stu-id="625e0-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="625e0-141">JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="625e0-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="625e0-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="625e0-143">MongoDB 匯出檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="625e0-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="625e0-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="625e0-145">CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="625e0-146">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="625e0-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="625e0-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="625e0-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="625e0-148">Blob</span><span class="sxs-lookup"><span data-stu-id="625e0-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="625e0-149">Azure Cosmos DB 集合</span><span class="sxs-lookup"><span data-stu-id="625e0-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="625e0-150">HBase</span><span class="sxs-lookup"><span data-stu-id="625e0-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="625e0-151">Azure Cosmos DB 大量匯入</span><span class="sxs-lookup"><span data-stu-id="625e0-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="625e0-152">Azure Cosmos DB 循序記錄匯入</span><span class="sxs-lookup"><span data-stu-id="625e0-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="625e0-153"><a id="JSON"></a>tooimport JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="625e0-154">hello JSON 檔案來源匯入工具選項可讓您 tooimport 其中一個或多個單一文件 JSON 檔案或將 JSON 檔案，其中每個包含 JSON 文件的陣列。</span><span class="sxs-lookup"><span data-stu-id="625e0-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="625e0-155">新增包含 JSON 檔案 tooimport 資料夾，您會有 hello 選項以遞迴方式搜尋子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="625e0-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![JSON 檔案來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/jsonsource.png)

<span data-ttu-id="625e0-157">以下是一些命令列範例 tooimport JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="625e0-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="625e0-158"><a id="MongoDB"></a>從 MongoDB tooimport</span><span class="sxs-lookup"><span data-stu-id="625e0-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="625e0-159">如果您要匯入 Support for MongoDB tooan Azure Cosmos DB 帳戶，請遵循這些[指示](mongodb-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="625e0-160">hello MongoDB 來源匯入工具選項可讓您從個別的 MongoDB 集合 tooimport 並選擇性地篩選使用查詢的文件及/或使用投影來修改 hello 文件結構。</span><span class="sxs-lookup"><span data-stu-id="625e0-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![MongoDB 來源選項的螢幕擷取畫面](./media/import-data/mongodbsource.png)

<span data-ttu-id="625e0-162">hello 連接字串是以標準 MongoDB 格式 hello:</span><span class="sxs-lookup"><span data-stu-id="625e0-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="625e0-163">使用 hello 確認命令 tooensure hello MongoDB hello 連接字串 欄位中指定的執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-164">輸入 hello hello 匯入資料的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="625e0-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="625e0-165">您可能會選擇性地指定，或者提供查詢檔 (例如 {pop: {$gt: 5000}}) 及/或投射 (例如 {loc:0}) tooboth 篩選器和圖形 hello 資料 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="625e0-166">以下是一些從 MongoDB 的命令列範例 tooimport:</span><span class="sxs-lookup"><span data-stu-id="625e0-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="625e0-167"><a id="MongoDBExport"></a>tooimport MongoDB 匯出檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="625e0-168">如果您要匯入 support for MongoDB。 tooan Azure Cosmos DB 帳戶，請遵循這些[指示](mongodb-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="625e0-169">hello MongoDB 匯出 JSON 檔案來源匯入工具選項可讓您 tooimport 其中一個或更多的 JSON 檔案產生從 hello mongoexport 公用程式。</span><span class="sxs-lookup"><span data-stu-id="625e0-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![MongoDB 匯出來源選項的螢幕擷取畫面](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="625e0-171">新增包含 MongoDB 匯出 JSON 檔案匯入的資料夾，您會有 hello 選項以遞迴方式搜尋子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="625e0-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="625e0-172">以下是從 MongoDB 匯出的命令列範例 tooimport JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="625e0-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="625e0-173"><a id="SQL"></a>從 SQL Server tooimport</span><span class="sxs-lookup"><span data-stu-id="625e0-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="625e0-174">hello SQL 來源匯入工具選項可讓您 tooimport 從個別的 SQL Server 資料庫，並選擇性地篩選 hello 記錄 toobe 匯入使用的查詢。</span><span class="sxs-lookup"><span data-stu-id="625e0-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="625e0-175">此外，您可以藉由指定巢狀的分隔符號 （稍後將詳細） 修改 hello 文件結構。</span><span class="sxs-lookup"><span data-stu-id="625e0-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![SQL 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/sqlexportsource.png)

<span data-ttu-id="625e0-177">hello hello 連接字串格式是 hello 標準 SQL 連接字串格式。</span><span class="sxs-lookup"><span data-stu-id="625e0-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="625e0-178">使用 hello 確認命令 tooensure hello hello 連接字串 欄位中指定的 SQL Server 執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-179">hello 巢狀方式置於 [分隔符號] 屬性匯入期間是使用的 toocreate 階層式關聯性 （子文件）。</span><span class="sxs-lookup"><span data-stu-id="625e0-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="625e0-180">請考慮下列 SQL 查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="625e0-180">Consider hello following SQL query:</span></span>

<bpt id="p1">*</bpt>select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'<ept id="p1">*</ept>

<span data-ttu-id="625e0-182">它會傳回下列結果 （部分） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="625e0-182">Which returns hello following (partial) results:</span></span>

![SQL 查詢結果的螢幕擷取畫面](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="625e0-184">請注意 Address.AddressType 等 Address.Location.StateProvinceName hello 別名。</span><span class="sxs-lookup"><span data-stu-id="625e0-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="625e0-185">藉由指定的巢狀分隔符號 '。 '、 hello 匯入工具建立位址，並匯入期間 hello Address.Location 子文件。</span><span class="sxs-lookup"><span data-stu-id="625e0-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="625e0-186">在 Azure Cosmos DB 中產生的文件範例如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="625e0-187">{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }</span><span class="sxs-lookup"><span data-stu-id="625e0-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="625e0-188">以下是一些命令列範例 tooimport，從 SQL Server:</span><span class="sxs-lookup"><span data-stu-id="625e0-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="625e0-189"><a id="CSV"></a>tooimport CSV 檔案和轉換 CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="625e0-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="625e0-190">hello CSV 檔案來源匯入工具選項可讓您 tooimport 一或多個 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="625e0-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="625e0-191">新增包含匯入 CSV 檔案的資料夾，您會有 hello 選項以遞迴方式搜尋子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="625e0-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![螢幕擷取畫面的 CSV 來源選項 CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="625e0-193">匯入期間，類似 toohello SQL 來源，hello 巢狀分隔符號屬性可能會使用的 toocreate 階層式關聯性 （子文件）。</span><span class="sxs-lookup"><span data-stu-id="625e0-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="625e0-194">請考慮下列 CSV 標頭資料列和資料列的 hello:</span><span class="sxs-lookup"><span data-stu-id="625e0-194">Consider hello following CSV header row and data rows:</span></span>

![螢幕擷取畫面的 CSV 範例記錄 CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="625e0-196">請注意 DomainInfo.Domain_Name 等 RedirectInfo.Redirecting hello 別名。</span><span class="sxs-lookup"><span data-stu-id="625e0-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="625e0-197">藉由指定的巢狀分隔符號 '。 ' hello 匯入工具會建立 DomainInfo，匯入期間 hello RedirectInfo 子文件。</span><span class="sxs-lookup"><span data-stu-id="625e0-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="625e0-198">在 Azure Cosmos DB 中產生的文件範例如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="625e0-199">*{"DomainInfo": {"Domain_Name":"ACUS.GOV"、"Domain_Name_Address":"http://www。ACUS.GOV"}，「 美國聯邦代理者 」: 「 系統管理會議的 hello 美國 」、 「 RedirectInfo": {」 重新導向 」:"0"、"Redirect_Destination":""}，"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="625e0-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="625e0-200">hello 匯入工具會嘗試 tooinfer 類型值的資訊未加引號之 CSV 檔案中 （加上引號的值會一律視為字串）。</span><span class="sxs-lookup"><span data-stu-id="625e0-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="625e0-201">Hello 順序中所識別的型別： 數字、 datetime、 布林值。</span><span class="sxs-lookup"><span data-stu-id="625e0-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="625e0-202">有兩個其他項目 toonote 關於 CSV 匯入：</span><span class="sxs-lookup"><span data-stu-id="625e0-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="625e0-203">根據預設，不具引號的值一律會針對定位點和空格進行修剪，而具有引號的值則會以原樣方式加以保留。</span><span class="sxs-lookup"><span data-stu-id="625e0-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="625e0-204">Hello Trim 加上引號的值核取方塊或 hello /s.TrimQuoted 命令列選項可以覆寫此行為。</span><span class="sxs-lookup"><span data-stu-id="625e0-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="625e0-205">根據預設，不具引號的 Null 會被視為 Null 值。</span><span class="sxs-lookup"><span data-stu-id="625e0-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="625e0-206">覆寫這個行為 （亦即視為不具引號的 null"null"字串） 以 hello Treat 不加引號的字串核取方塊 hello /s.NoUnquotedNulls 命令列選項或為 NULL。</span><span class="sxs-lookup"><span data-stu-id="625e0-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="625e0-207">以下是 CSV 匯入的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="625e0-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="625e0-208"><a id="AzureTableSource"></a>從 Azure 資料表儲存體 tooimport</span><span class="sxs-lookup"><span data-stu-id="625e0-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="625e0-209">hello Azure 資料表儲存體來源匯入工具選項可讓您從個別的 Azure 資料表儲存體資料表 tooimport，並選擇性地篩選 hello 資料表實體 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="625e0-210">請注意，您不可使用 hello 資料移轉工具 tooimport Azure 資料表儲存體資料到 Azure Cosmos DB hello 表格 API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="625e0-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="625e0-211">目前支援僅匯入 tooAzure Cosmos DB hello DocumentDB API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="625e0-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Azure 資料表儲存體來源選項的螢幕擷取畫面](./media/import-data/azuretablesource.png)

<span data-ttu-id="625e0-213">hello 的 hello Azure 資料表儲存體連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="625e0-214">使用 hello 確認命令 tooensure hello hello 連接字串 欄位中指定的 Azure 資料表儲存體執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-215">輸入 hello 名稱 hello Azure 匯入資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="625e0-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="625e0-216">您可以選擇性地指定 [篩選器](https://msdn.microsoft.com/library/azure/ff683669.aspx)。</span><span class="sxs-lookup"><span data-stu-id="625e0-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="625e0-217">hello Azure 資料表儲存體來源匯入工具選項具有下列其他選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="625e0-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="625e0-218">包含內部欄位</span><span class="sxs-lookup"><span data-stu-id="625e0-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="625e0-219">全部 - 包括所有內部欄位 (PartitionKey、RowKey 和 Timestamp)</span><span class="sxs-lookup"><span data-stu-id="625e0-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="625e0-220">無 - 排除所有內部欄位</span><span class="sxs-lookup"><span data-stu-id="625e0-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="625e0-221">RowKey-只包含 hello RowKey 欄位</span><span class="sxs-lookup"><span data-stu-id="625e0-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="625e0-222">選取資料行</span><span class="sxs-lookup"><span data-stu-id="625e0-222">Select Columns</span></span>
   1. <span data-ttu-id="625e0-223">Azure 資料表儲存體篩選器不支援投影。</span><span class="sxs-lookup"><span data-stu-id="625e0-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="625e0-224">如果您想 tooonly 匯入特定 Azure 資料表實體屬性，請將其加入 toohello 選取資料行清單。</span><span class="sxs-lookup"><span data-stu-id="625e0-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="625e0-225">其他所有實體屬性都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="625e0-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="625e0-226">以下是命令列範例 tooimport 從 Azure 資料表儲存體：</span><span class="sxs-lookup"><span data-stu-id="625e0-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="625e0-227"><a id="DynamoDBSource"></a>從 Amazon DynamoDB tooimport</span><span class="sxs-lookup"><span data-stu-id="625e0-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="625e0-228">hello Amazon DynamoDB 來源匯入工具選項可讓您從個別的 Amazon DynamoDB 資料表 tooimport，並選擇性地篩選 hello 實體 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="625e0-229">會提供數個範本，讓設定匯入盡量簡化。</span><span class="sxs-lookup"><span data-stu-id="625e0-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Amazon DynamoDB 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="625e0-232">hello 的 hello Amazon DynamoDB 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="625e0-233">使用 hello 確認命令 tooensure hello Amazon DynamoDB hello 連接字串 欄位中指定的執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-234">以下是從 Amazon DynamoDB 命令列範例 tooimport:</span><span class="sxs-lookup"><span data-stu-id="625e0-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="625e0-235"><a id="BlobImport"></a>從 Azure Blob 儲存體 tooimport 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="625e0-236">hello JSON 檔案、 MongoDB 匯出檔案和 CSV 檔案來源匯入工具選項可讓您 tooimport 從 Azure Blob 儲存體的一或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="625e0-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="625e0-237">指定 Blob 容器 URL 和帳戶金鑰之後, 直接提供規則運算式 tooselect hello 檔案 tooimport。</span><span class="sxs-lookup"><span data-stu-id="625e0-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Blob 檔案來源選項的螢幕擷取畫面](./media/import-data/blobsource.png)

<span data-ttu-id="625e0-239">以下是命令列範例 tooimport JSON 檔案從 Azure Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="625e0-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="625e0-240"><a id="DocumentDBSource"></a>從 Azure Cosmos DB DocumentDB API 集合 tooimport</span><span class="sxs-lookup"><span data-stu-id="625e0-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="625e0-241">hello Azure Cosmos DB 來源匯入工具選項可讓您從一或多個 Azure Cosmos DB 集合 tooimport 資料，並選擇性地篩選使用查詢的文件。</span><span class="sxs-lookup"><span data-stu-id="625e0-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Azure Cosmos DB 來源選項的螢幕擷取畫面](./media/import-data/documentdbsource.png)

<span data-ttu-id="625e0-243">hello 的 hello Azure Cosmos DB 的連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="625e0-244">hello Azure Cosmos DB 帳戶連接字串可從擷取的 hello 金鑰刀鋒視窗中的 hello Azure 入口網站中所述[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md)，不過 hello hello 資料庫名稱必須附加 toobe toohellohello 遵循格式中的連接字串：</span><span class="sxs-lookup"><span data-stu-id="625e0-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="625e0-245">使用 hello 確認命令 tooensure hello Azure Cosmos DB hello 連接字串 欄位中指定的執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-246">單一 Azure Cosmos DB 集合，從 tooimport 輸入 hello hello 匯入資料的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="625e0-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="625e0-247">從多個 Azure Cosmos DB 集合，tooimport 提供規則運算式 toomatch 一或多個集合的名稱 (例如 collection01 | collection02 | collection03)。</span><span class="sxs-lookup"><span data-stu-id="625e0-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="625e0-248">您可能會選擇性地指定，或提供的查詢 tooboth 篩選檔圖案和 hello 資料 toobe 匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="625e0-249">因為 hello 集合欄位接受規則運算式，如果您要匯入從單一集合，其名稱包含規則運算式的字元，然後這些字元必須逸出據此。</span><span class="sxs-lookup"><span data-stu-id="625e0-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="625e0-250">hello Azure Cosmos DB 來源匯入工具選項已經 hello 下列進階選項：</span><span class="sxs-lookup"><span data-stu-id="625e0-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="625e0-251">包含內部欄位： 指定在 hello tooinclude Azure Cosmos DB 文件系統屬性匯出 (例如 _rid，_ts)。</span><span class="sxs-lookup"><span data-stu-id="625e0-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="625e0-252">失敗的重試次數： 指定 tooretry hello 連接 tooAzure Cosmos DB 在暫時性失敗 （例如網路連線中斷） 的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="625e0-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="625e0-253">重試間隔： 指定多久 toowait 之間發生暫時性失敗 （例如網路連線中斷） 的 hello 連接 tooAzure Cosmos DB 重試一次。</span><span class="sxs-lookup"><span data-stu-id="625e0-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="625e0-254">連接模式： 指定 hello 連線模式 toouse 搭配 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="625e0-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="625e0-255">hello 可用的選項是 DirectTcp、 DirectHttps 和閘道。</span><span class="sxs-lookup"><span data-stu-id="625e0-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="625e0-256">hello 直接連線模式速度較快，而 hello 閘道模式是多個防火牆易記，因為它只會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="625e0-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 來源進階選項的螢幕擷取畫面](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="625e0-258">hello 匯入工具的預設值 tooconnection 模式 DirectTcp。</span><span class="sxs-lookup"><span data-stu-id="625e0-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="625e0-259">如果您遇到防火牆問題，請切換 tooconnection 模式閘道，因為它只需要連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="625e0-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="625e0-260">以下是一些命令列範例 tooimport，從 Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="625e0-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="625e0-261">hello Azure Cosmos DB 的資料匯入的工具也支援匯入的資料從 hello [Azure Cosmos DB 模擬器](local-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="625e0-262">當從本機模擬器，匯入資料，設定 hello 端點太`https://localhost:<port>`。</span><span class="sxs-lookup"><span data-stu-id="625e0-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="625e0-263"><a id="HBaseSource"></a>從 HBase tooimport</span><span class="sxs-lookup"><span data-stu-id="625e0-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="625e0-264">hello HBase 來源匯入工具選項可讓您 tooimport HBase 資料表的資料，並選擇性地篩選 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="625e0-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="625e0-265">會提供數個範本，讓設定匯入盡量簡化。</span><span class="sxs-lookup"><span data-stu-id="625e0-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![HBase 檔案來源選項的螢幕擷取畫面](./media/import-data/hbasesource1.png)

![HBase 檔案來源選項的螢幕擷取畫面](./media/import-data/hbasesource2.png)

<span data-ttu-id="625e0-268">hello 的 hello HBase Stargate 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="625e0-269">使用 hello 確認命令 tooensure hello HBase hello 連接字串 欄位中指定的執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-270">以下是從 HBase 命令列範例 tooimport:</span><span class="sxs-lookup"><span data-stu-id="625e0-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="625e0-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API （大量匯入）</span><span class="sxs-lookup"><span data-stu-id="625e0-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="625e0-272">hello Azure Cosmos DB 大量匯入工具，可讓您從任何 hello 可用的來源選項，請使用 Azure Cosmos DB 預存程序以提升效率 tooimport。</span><span class="sxs-lookup"><span data-stu-id="625e0-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="625e0-273">hello 工具支援匯入 tooone 單一分割 Azure Cosmos DB 集合，以及在多個單一資料分割 Azure Cosmos DB 集合分割資料分割的分區化匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="625e0-274">如需分割資料的詳細資訊，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="625e0-275">hello 工具會建立、 執行，然後刪除 hello 目標清查中的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="625e0-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Azure Cosmos DB 大量選項的螢幕擷取畫面](./media/import-data/documentdbbulk.png)

<span data-ttu-id="625e0-277">hello 的 hello Azure Cosmos DB 的連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="625e0-278">hello Azure Cosmos DB 帳戶連接字串可從擷取的 hello 金鑰刀鋒視窗中的 hello Azure 入口網站中所述[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md)，不過 hello hello 資料庫名稱必須附加 toobe toohellohello 遵循格式中的連接字串：</span><span class="sxs-lookup"><span data-stu-id="625e0-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="625e0-279">使用 hello 確認命令 tooensure hello Azure Cosmos DB hello 連接字串 欄位中指定的執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-280">tooimport tooa 單一集合中，輸入 hello 名稱 hello 集合 toowhich 資料將匯入和按一下 hello [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="625e0-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="625e0-281">tooimport toomultiple 集合、 個別輸入每個集合的名稱或使用下列語法 toospecify hello 多個集合： *collection_prefix*[start 索引-結束索引]。</span><span class="sxs-lookup"><span data-stu-id="625e0-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="625e0-282">當指定多個集合，透過 hello 上述語法，請記住 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="625e0-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="625e0-283">僅支援整數範圍的名稱模式。</span><span class="sxs-lookup"><span data-stu-id="625e0-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="625e0-284">比方說，指定集合 [0-3] 將會產生下列集合的 hello: collection0，collection1，collection2，collection3。</span><span class="sxs-lookup"><span data-stu-id="625e0-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="625e0-285">您可以使用縮寫的語法：collection[3] 將發出一組與步驟 1 中所述相同的集合。</span><span class="sxs-lookup"><span data-stu-id="625e0-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="625e0-286">您可以提供一個以上的替代項目。</span><span class="sxs-lookup"><span data-stu-id="625e0-286">More than one substitution can be provided.</span></span> <span data-ttu-id="625e0-287">例如，collection[0-1] [0-9] 將產生 20 個開頭為零的集合名稱 (collection01、..02、..03)。</span><span class="sxs-lookup"><span data-stu-id="625e0-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="625e0-288">一旦 hello 集合名稱已指定，則選擇 hello 的 hello 清查 (400 Ru too10，000 RUs) 所需的輸送量。</span><span class="sxs-lookup"><span data-stu-id="625e0-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="625e0-289">為了達到最佳的匯入效能，請選擇較高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="625e0-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="625e0-290">如需效能層級的詳細資訊，請參閱 [Azure Cosmos DB 中的效能層級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="625e0-291">hello 效能輸送量設定僅適用於 toocollection 建立。</span><span class="sxs-lookup"><span data-stu-id="625e0-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="625e0-292">如果 hello 指定集合已經存在，將不會修改其輸送量。</span><span class="sxs-lookup"><span data-stu-id="625e0-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="625e0-293">當匯入 toomultiple 集合，hello 匯入工具會支援基礎的雜湊分區化。</span><span class="sxs-lookup"><span data-stu-id="625e0-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="625e0-294">在此案例中，指定您想 toouse hello 資料分割索引鍵為 hello 文件屬性 （如果空白的資料分割索引鍵，文件將分區化隨機跨 hello 目標集合）。</span><span class="sxs-lookup"><span data-stu-id="625e0-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="625e0-295">您可以選擇性地指定 hello 匯入來源中的哪一個欄位應該做為 hello Azure Cosmos DB 文件的 id 屬性期間 hello 匯入 （請注意，如果文件未包含此屬性，則 hello 匯入工具會產生 hello id 屬性值為 GUID）。</span><span class="sxs-lookup"><span data-stu-id="625e0-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="625e0-296">匯入期間有數個可用的進階選項。</span><span class="sxs-lookup"><span data-stu-id="625e0-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="625e0-297">首先，而 hello 工具包含預設大量匯入的預存程序 (BulkInsert.js)，您可以選擇 toospecify 匯入預存程序：</span><span class="sxs-lookup"><span data-stu-id="625e0-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Azure Cosmos DB 大量插入 sproc 選項的螢幕擷取畫面](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="625e0-299">此外，匯入日期類型時 (例如從 SQL Server 或 MongoDB)，有三種匯入選項可供選擇：</span><span class="sxs-lookup"><span data-stu-id="625e0-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB 日期時間匯入選項的螢幕擷取畫面](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="625e0-301">字串：保存為字串值</span><span class="sxs-lookup"><span data-stu-id="625e0-301">String: Persist as a string value</span></span>
* <span data-ttu-id="625e0-302">Epoch：保存為 Epoch 數值</span><span class="sxs-lookup"><span data-stu-id="625e0-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="625e0-303">兩者：保存字串和 Epoch 數值。</span><span class="sxs-lookup"><span data-stu-id="625e0-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="625e0-304">這個選項會建立子文件，例如："date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="625e0-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="625e0-305">hello Azure Cosmos DB 大量匯入工具具有 hello 下列其他進階選項：</span><span class="sxs-lookup"><span data-stu-id="625e0-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="625e0-306">批次大小： hello 工具的預設值 tooa 批次大小為 50。</span><span class="sxs-lookup"><span data-stu-id="625e0-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="625e0-307">如果匯入的 hello 文件 toobe 很大，請考慮降低 hello 批次大小。</span><span class="sxs-lookup"><span data-stu-id="625e0-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="625e0-308">相反地，如果匯入的 hello 文件 toobe 很小，請考慮引發 hello 批次大小。</span><span class="sxs-lookup"><span data-stu-id="625e0-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="625e0-309">指令碼大小上限 （位元組）： hello 工具預設值為 512 KB 的 tooa 最大指令碼大小</span><span class="sxs-lookup"><span data-stu-id="625e0-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="625e0-310">停用自動 Id 產生： 如果匯入每個文件 toobe 包含識別碼欄位，然後選取此選項可提升效能。</span><span class="sxs-lookup"><span data-stu-id="625e0-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="625e0-311">遺漏唯一識別碼欄位的文件將不會被匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="625e0-312">更新現有文件： hello 工具的預設值 toonot 取代現有的文件識別碼相衝突。</span><span class="sxs-lookup"><span data-stu-id="625e0-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="625e0-313">如果選取此選項，將會允許在識別碼相符時覆寫現有的文件。</span><span class="sxs-lookup"><span data-stu-id="625e0-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="625e0-314">對於會更新現有文件的已排定資料移轉來說，這項功能相當有用。</span><span class="sxs-lookup"><span data-stu-id="625e0-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="625e0-315">失敗的重試次數： 指定 tooretry hello 連接 tooAzure Cosmos DB 在暫時性失敗 （例如網路連線中斷） 的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="625e0-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="625e0-316">重試間隔： 指定多久 toowait 之間發生暫時性失敗 （例如網路連線中斷） 的 hello 連接 tooAzure Cosmos DB 重試一次。</span><span class="sxs-lookup"><span data-stu-id="625e0-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="625e0-317">連接模式： 指定 hello 連線模式 toouse 搭配 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="625e0-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="625e0-318">hello 可用的選項是 DirectTcp、 DirectHttps 和閘道。</span><span class="sxs-lookup"><span data-stu-id="625e0-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="625e0-319">hello 直接連線模式速度較快，而 hello 閘道模式是多個防火牆易記，因為它只會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="625e0-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 大量匯入進階選項的螢幕擷取畫面](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="625e0-321">hello 匯入工具的預設值 tooconnection 模式 DirectTcp。</span><span class="sxs-lookup"><span data-stu-id="625e0-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="625e0-322">如果您遇到防火牆問題，請切換 tooconnection 模式閘道，因為它只需要連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="625e0-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="625e0-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API （循序記錄匯入）</span><span class="sxs-lookup"><span data-stu-id="625e0-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="625e0-324">hello Azure Cosmos DB 循序記錄匯入工具，可讓您從任何記錄為基礎的 hello 可用的來源選項 tooimport。</span><span class="sxs-lookup"><span data-stu-id="625e0-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="625e0-325">如果您要匯入 tooan 已達到其配額的預存程序的現有集合，您可能會選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="625e0-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="625e0-326">hello 工具支援匯入 tooa 單一 Azure Cosmos DB 集合 （單一資料分割和多個資料分割），以及在多個單一資料分割和/或多個資料分割的 Azure Cosmos DB 集合分割資料分割的分區化匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="625e0-327">如需分割資料的詳細資訊，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Azure Cosmos DB 循序記錄匯入選項的螢幕擷取畫面](./media/import-data/documentdbsequential.png)

<span data-ttu-id="625e0-329">hello 的 hello Azure Cosmos DB 的連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="625e0-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="625e0-330">hello Azure Cosmos DB 帳戶連接字串可從擷取的 hello 金鑰刀鋒視窗中的 hello Azure 入口網站中所述[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md)，不過 hello hello 資料庫名稱必須附加 toobe toohellohello 遵循格式中的連接字串：</span><span class="sxs-lookup"><span data-stu-id="625e0-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="625e0-331">使用 hello 確認命令 tooensure hello Azure Cosmos DB hello 連接字串 欄位中指定的執行個體，可以存取。</span><span class="sxs-lookup"><span data-stu-id="625e0-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="625e0-332">tooimport tooa 單一集合中，輸入 hello 名稱 hello 集合 toowhich 資料將匯入和按一下 hello [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="625e0-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="625e0-333">tooimport toomultiple 集合、 個別輸入每個集合的名稱或使用下列語法 toospecify hello 多個集合： *collection_prefix*[start 索引-結束索引]。</span><span class="sxs-lookup"><span data-stu-id="625e0-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="625e0-334">當指定多個集合，透過 hello 上述語法，請記住 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="625e0-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="625e0-335">僅支援整數範圍的名稱模式。</span><span class="sxs-lookup"><span data-stu-id="625e0-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="625e0-336">比方說，指定集合 [0-3] 將會產生下列集合的 hello: collection0，collection1，collection2，collection3。</span><span class="sxs-lookup"><span data-stu-id="625e0-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="625e0-337">您可以使用縮寫的語法：collection[3] 將發出一組與步驟 1 中所述相同的集合。</span><span class="sxs-lookup"><span data-stu-id="625e0-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="625e0-338">您可以提供一個以上的替代項目。</span><span class="sxs-lookup"><span data-stu-id="625e0-338">More than one substitution can be provided.</span></span> <span data-ttu-id="625e0-339">例如，collection[0-1] [0-9] 將產生 20 個開頭為零的集合名稱 (collection01、..02、..03)。</span><span class="sxs-lookup"><span data-stu-id="625e0-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="625e0-340">一旦 hello 集合名稱已指定，則選擇 hello 的 hello 清查 (400 Ru too250，000 RUs) 所需的輸送量。</span><span class="sxs-lookup"><span data-stu-id="625e0-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="625e0-341">為了達到最佳的匯入效能，請選擇較高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="625e0-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="625e0-342">如需效能層級的詳細資訊，請參閱 [Azure Cosmos DB 中的效能層級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="625e0-343">任何匯入與輸送量 toocollections > 10,000 RUs 需要資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="625e0-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="625e0-344">如果您選擇 toohave 以上 250,000 RUs，您將需要 toofile hello 入口 toohave 增加您的帳戶的要求。</span><span class="sxs-lookup"><span data-stu-id="625e0-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="625e0-345">hello 輸送量設定僅適用於 toocollection 建立。</span><span class="sxs-lookup"><span data-stu-id="625e0-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="625e0-346">如果 hello 指定集合已經存在，將不會修改其輸送量。</span><span class="sxs-lookup"><span data-stu-id="625e0-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="625e0-347">當匯入 toomultiple 集合，hello 匯入工具會支援基礎的雜湊分區化。</span><span class="sxs-lookup"><span data-stu-id="625e0-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="625e0-348">在此案例中，指定您想 toouse hello 資料分割索引鍵為 hello 文件屬性 （如果空白的資料分割索引鍵，文件將分區化隨機跨 hello 目標集合）。</span><span class="sxs-lookup"><span data-stu-id="625e0-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="625e0-349">您可以選擇性地指定 hello 匯入來源中的哪一個欄位應該做為 hello Azure Cosmos DB 文件的 id 屬性期間 hello 匯入 （請注意，如果文件未包含此屬性，則 hello 匯入工具會產生 hello id 屬性值為 GUID）。</span><span class="sxs-lookup"><span data-stu-id="625e0-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="625e0-350">匯入期間有數個可用的進階選項。</span><span class="sxs-lookup"><span data-stu-id="625e0-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="625e0-351">首先，匯入日期類型時 (例如從 SQL Server 或 MongoDB)，有三種匯入選項可供選擇：</span><span class="sxs-lookup"><span data-stu-id="625e0-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB 日期時間匯入選項的螢幕擷取畫面](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="625e0-353">字串：保存為字串值</span><span class="sxs-lookup"><span data-stu-id="625e0-353">String: Persist as a string value</span></span>
* <span data-ttu-id="625e0-354">Epoch：保存為 Epoch 數值</span><span class="sxs-lookup"><span data-stu-id="625e0-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="625e0-355">兩者：保存字串和 Epoch 數值。</span><span class="sxs-lookup"><span data-stu-id="625e0-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="625e0-356">這個選項會建立子文件，例如："date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="625e0-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="625e0-357">hello Azure Cosmos DB 循序記錄匯入工具具有 hello 下列其他進階選項：</span><span class="sxs-lookup"><span data-stu-id="625e0-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="625e0-358">平行要求的數目： hello 工具預設 too2 平行要求。</span><span class="sxs-lookup"><span data-stu-id="625e0-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="625e0-359">如果匯入的 hello 文件 toobe 很小，請考慮引發 hello 平行要求的數目。</span><span class="sxs-lookup"><span data-stu-id="625e0-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="625e0-360">請注意，如果這個數字太多，就會引發 hello 匯入可能會發生節流。</span><span class="sxs-lookup"><span data-stu-id="625e0-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="625e0-361">停用自動 Id 產生： 如果匯入每個文件 toobe 包含識別碼欄位，然後選取此選項可提升效能。</span><span class="sxs-lookup"><span data-stu-id="625e0-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="625e0-362">遺漏唯一識別碼欄位的文件將不會被匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="625e0-363">更新現有文件： hello 工具的預設值 toonot 取代現有的文件識別碼相衝突。</span><span class="sxs-lookup"><span data-stu-id="625e0-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="625e0-364">如果選取此選項，將會允許在識別碼相符時覆寫現有的文件。</span><span class="sxs-lookup"><span data-stu-id="625e0-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="625e0-365">對於會更新現有文件的已排定資料移轉來說，這項功能相當有用。</span><span class="sxs-lookup"><span data-stu-id="625e0-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="625e0-366">失敗的重試次數： 指定 tooretry hello 連接 tooAzure Cosmos DB 在暫時性失敗 （例如網路連線中斷） 的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="625e0-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="625e0-367">重試間隔： 指定多久 toowait 之間發生暫時性失敗 （例如網路連線中斷） 的 hello 連接 tooAzure Cosmos DB 重試一次。</span><span class="sxs-lookup"><span data-stu-id="625e0-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="625e0-368">連接模式： 指定 hello 連線模式 toouse 搭配 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="625e0-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="625e0-369">hello 可用的選項是 DirectTcp、 DirectHttps 和閘道。</span><span class="sxs-lookup"><span data-stu-id="625e0-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="625e0-370">hello 直接連線模式速度較快，而 hello 閘道模式是多個防火牆易記，因為它只會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="625e0-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 循序記錄匯入進階選項的螢幕擷取畫面](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="625e0-372">hello 匯入工具的預設值 tooconnection 模式 DirectTcp。</span><span class="sxs-lookup"><span data-stu-id="625e0-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="625e0-373">如果您遇到防火牆問題，請切換 tooconnection 模式閘道，因為它只需要連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="625e0-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="625e0-374"><a id="IndexingPolicy"></a>建立 Azure Cosmos DB 集合時指定編製索引原則</span><span class="sxs-lookup"><span data-stu-id="625e0-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="625e0-375">當您允許 hello 移轉工具 toocreate 集合匯入期間時，您可以指定 hello 的 hello 集合的編製索引原則。</span><span class="sxs-lookup"><span data-stu-id="625e0-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="625e0-376">在 [進階選項 > 一節的 hello Azure Cosmos DB 大量匯入和 Azure Cosmos DB 循序記錄選項的 hello，瀏覽 toohello 編製索引原則] 區段中。</span><span class="sxs-lookup"><span data-stu-id="625e0-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Azure Cosmos DB 編製索引原則進階選項的螢幕擷取畫面](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="625e0-378">使用 hello 編製索引原則的進階選項，您可以選取索引的原則檔，以手動方式輸入編製索引的原則，或選取從一組預設範本 （以滑鼠右鍵按一下中編製索引原則文字方塊中的 hello）。</span><span class="sxs-lookup"><span data-stu-id="625e0-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="625e0-379">hello hello 工具提供的原則範本是：</span><span class="sxs-lookup"><span data-stu-id="625e0-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="625e0-380">預設值。</span><span class="sxs-lookup"><span data-stu-id="625e0-380">Default.</span></span> <span data-ttu-id="625e0-381">當您使用 ORDER BY、範圍和數字的相等查詢針對字串進行相等查詢時，這是最佳的原則。</span><span class="sxs-lookup"><span data-stu-id="625e0-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="625e0-382">這個原則的索引儲存空間負擔比範圍低。</span><span class="sxs-lookup"><span data-stu-id="625e0-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="625e0-383">範圍。</span><span class="sxs-lookup"><span data-stu-id="625e0-383">Range.</span></span> <span data-ttu-id="625e0-384">當您使用 ORDER BY、範圍以及數字和字串的相等查詢時，這是最佳的原則。</span><span class="sxs-lookup"><span data-stu-id="625e0-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="625e0-385">這個原則的索引儲存空間負擔比預設或雜湊高。</span><span class="sxs-lookup"><span data-stu-id="625e0-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Azure Cosmos DB 編製索引原則進階選項的螢幕擷取畫面](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="625e0-387">如果您未指定編製索引的原則，將會套用 hello 預設原則。</span><span class="sxs-lookup"><span data-stu-id="625e0-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="625e0-388">如需編製索引原則的詳細資訊，請參閱 [Azure Cosmos DB 編製索引原則](indexing-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="625e0-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="625e0-389">匯出 tooJSON 檔案</span><span class="sxs-lookup"><span data-stu-id="625e0-389">Export tooJSON file</span></span>
<span data-ttu-id="625e0-390">hello Azure Cosmos DB JSON 匯出工具可讓您 tooexport 任何 hello 可用的來源選項 tooa JSON 檔案，其中包含 JSON 文件的陣列。</span><span class="sxs-lookup"><span data-stu-id="625e0-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="625e0-391">hello 工具將會處理 hello 匯出，或您可以選擇 tooview hello 產生移轉命令，然後自行執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="625e0-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="625e0-392">在本機或 Azure Blob 儲存體中，可能會儲存 hello 產生的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="625e0-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Azure Cosmos DB JSON 本機檔案匯出選項的螢幕擷取畫面](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob 儲存體匯出選項的螢幕擷取畫面](./media/import-data/jsontarget2.png)

<span data-ttu-id="625e0-395">您可以選擇性地選擇 tooprettify hello 產生 JSON，會增加 hello hello 產生的文件大小，而使 hello 內容更多的人們可讀取。</span><span class="sxs-lookup"><span data-stu-id="625e0-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="625e0-396">進階組態</span><span class="sxs-lookup"><span data-stu-id="625e0-396">Advanced configuration</span></span>
<span data-ttu-id="625e0-397">在 hello 進階的組態畫面中，指定您想要寫入的任何錯誤 hello 記錄檔案 toowhich hello 位置。</span><span class="sxs-lookup"><span data-stu-id="625e0-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="625e0-398">hello 下列規則適用於 toothis 頁面：</span><span class="sxs-lookup"><span data-stu-id="625e0-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="625e0-399">如果未提供檔案名稱，所有的錯誤將傳回 hello [結果] 頁面。</span><span class="sxs-lookup"><span data-stu-id="625e0-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="625e0-400">如果沒有目錄提供檔案名稱，然後 hello 檔案會建立 （或覆寫） hello 目前環境的目錄中。</span><span class="sxs-lookup"><span data-stu-id="625e0-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="625e0-401">如果您選取的現有檔案，然後 hello 檔案將會覆寫，沒有附加選項。</span><span class="sxs-lookup"><span data-stu-id="625e0-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="625e0-402">然後，選擇是否 toolog 所有中的重大，或沒有錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="625e0-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="625e0-403">最後，決定螢幕傳輸訊息上的 hello 與它進行的更新頻率。</span><span class="sxs-lookup"><span data-stu-id="625e0-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="625e0-404">確認匯入設定及檢視命令列</span><span class="sxs-lookup"><span data-stu-id="625e0-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="625e0-405">指定來源資訊、 目標資訊以及進階的組態之後, 檢閱 hello 移轉摘要並，選擇性地檢視/複製 hello 產生 （複製 hello 命令是有用的 tooautomate 匯入作業） 的移轉命令：</span><span class="sxs-lookup"><span data-stu-id="625e0-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![摘要畫面的螢幕擷取畫面](./media/import-data/summary.png)
   
    ![摘要畫面的螢幕擷取畫面](./media/import-data/summarycommand.png)
2. <span data-ttu-id="625e0-408">在您滿意來源和目標選項之後，請按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="625e0-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="625e0-409">hello 已耗用時間、 傳送的計數，以及 （如果您並未提供 hello 進階組態中的檔案名稱） 的失敗資訊會隨著 hello 匯入正在進行更新。</span><span class="sxs-lookup"><span data-stu-id="625e0-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="625e0-410">完成後，您可以匯出 hello 結果 (例如 toodeal 解決任何匯入失敗)。</span><span class="sxs-lookup"><span data-stu-id="625e0-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Azure Cosmos DB JSON 匯出選項的螢幕擷取畫面](./media/import-data/viewresults.png)
3. <span data-ttu-id="625e0-412">保留 hello 現有的設定 （例如連接字串資訊、 來源和目標選擇等） 或重設所有的值，您也可能會啟動新的匯入。</span><span class="sxs-lookup"><span data-stu-id="625e0-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Azure Cosmos DB JSON 匯出選項的螢幕擷取畫面](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="625e0-414">後續步驟</span><span class="sxs-lookup"><span data-stu-id="625e0-414">Next steps</span></span>

<span data-ttu-id="625e0-415">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="625e0-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="625e0-416">安裝 hello 資料移轉工具</span><span class="sxs-lookup"><span data-stu-id="625e0-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="625e0-417">已從不同的資料來源匯入資料</span><span class="sxs-lookup"><span data-stu-id="625e0-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="625e0-418">從 Azure Cosmos DB tooJSON 匯出</span><span class="sxs-lookup"><span data-stu-id="625e0-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="625e0-419">您現在可以繼續 toohello 下一個教學課程，並了解如何使用 Azure Cosmos DB tooquery 資料。</span><span class="sxs-lookup"><span data-stu-id="625e0-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="625e0-420">如何 tooquery 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="625e0-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
