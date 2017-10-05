---
title: "Azure Cosmos DB 的資料庫移轉工具 | Microsoft Docs"
description: "了解如何使用開放原始碼 Azure Cosmos DB 資料移轉工具，將各種來源的資料 (包括 MongoDB、SQL Server、資料表儲存體、Amazon DynamoDB、CSV 及 JSON 檔案) 匯入到 Azure Cosmos DB。 將 CSV 轉換成 JSON。"
keywords: "csv 轉換成 json, 資料庫移轉工具, 將 csv 轉換成 json"
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
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="2213d-105">如何將資料匯入到 DocumentDB API 的 Azure Cosmos DB？</span><span class="sxs-lookup"><span data-stu-id="2213d-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="2213d-106">本教學課程提供使用 Azure Cosmos DB：DocumentDB API 資料移轉工具的相關指示，可將資料從各種來源 (包括 JSON 檔案、CSV 檔案、SQL、MongoDB、Azure 資料表儲存體、Amazon DynamoDB 及 Azure Cosmos DB DocumentDB API 集合) 匯入到要與 Azure Cosmos DB 和 DocumentDB API 搭配使用的集合。</span><span class="sxs-lookup"><span data-stu-id="2213d-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="2213d-107">針對 DocumentDB API 從單一分割區集合移轉到多重分割區集合時，也可以使用資料移轉工具。</span><span class="sxs-lookup"><span data-stu-id="2213d-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="2213d-108">將資料匯入到 Azure Cosmos DB 來與 DocumentDB API 搭配使用時，僅適用資料移轉工具。</span><span class="sxs-lookup"><span data-stu-id="2213d-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="2213d-109">目前不支援匯入資料來與資料表 API 或圖形 API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="2213d-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="2213d-110">若要匯入資料來與 MongoDB API 搭配使用，請參閱 [Azure Cosmos DB︰如何移轉適用於 MongoDB API 的資料？](mongodb-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="2213d-111">本教學課程涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="2213d-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2213d-112">安裝資料移轉工具</span><span class="sxs-lookup"><span data-stu-id="2213d-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="2213d-113">從不同的資料來源匯入資料</span><span class="sxs-lookup"><span data-stu-id="2213d-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="2213d-114">從 Azure Cosmos DB 匯出到 JSON</span><span class="sxs-lookup"><span data-stu-id="2213d-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="2213d-115"><a id="Prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="2213d-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="2213d-116">在依照本文中的指示進行之前，請確定已安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="2213d-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="2213d-117">[Microsoft.NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="2213d-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="2213d-118"><a id="Overviewl"></a>資料移轉工具概觀</span><span class="sxs-lookup"><span data-stu-id="2213d-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="2213d-119">資料移轉工具是一個開放原始碼解決方案，可將資料從各種來源匯入到 Azure Cosmos DB，來源包括：</span><span class="sxs-lookup"><span data-stu-id="2213d-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="2213d-120">JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-120">JSON files</span></span>
* <span data-ttu-id="2213d-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="2213d-121">MongoDB</span></span>
* <span data-ttu-id="2213d-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="2213d-122">SQL Server</span></span>
* <span data-ttu-id="2213d-123">CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-123">CSV files</span></span>
* <span data-ttu-id="2213d-124">Azure 資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="2213d-124">Azure Table storage</span></span>
* <span data-ttu-id="2213d-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="2213d-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="2213d-126">HBase</span><span class="sxs-lookup"><span data-stu-id="2213d-126">HBase</span></span>
* <span data-ttu-id="2213d-127">Azure Cosmos DB 集合</span><span class="sxs-lookup"><span data-stu-id="2213d-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="2213d-128">雖然匯入工具包括圖形化使用者介面 (dtui.exe)，您也可以從命令列 (dt.exe) 驅動此工具。</span><span class="sxs-lookup"><span data-stu-id="2213d-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="2213d-129">事實上，在透過 UI 設定匯入之後，有一個選項可以輸出相關聯的命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="2213d-130">表格式來源資料 (例如 SQL Server 或 CSV 檔案) 可以進行轉換，以致可以在匯入期間建立階層式關聯性 (子文件)。</span><span class="sxs-lookup"><span data-stu-id="2213d-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="2213d-131">繼續閱讀以深入了解來源選項、從每個來源匯入的範例命令列、目標選項，以及檢視匯入結果。</span><span class="sxs-lookup"><span data-stu-id="2213d-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="2213d-132"><a id="Install"></a>安裝資料移轉工具</span><span class="sxs-lookup"><span data-stu-id="2213d-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="2213d-133">您可以在 GitHub 上的[此存放庫](https://github.com/azure/azure-documentdb-datamigrationtool)中找到移轉工具的原始程式碼，並可以從 [Microsoft 下載中心](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)取得編譯版本。</span><span class="sxs-lookup"><span data-stu-id="2213d-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="2213d-134">您可以編譯解決方案，或直接下載編譯版本並將它解壓縮至選擇的目錄。</span><span class="sxs-lookup"><span data-stu-id="2213d-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="2213d-135">然後執行：</span><span class="sxs-lookup"><span data-stu-id="2213d-135">Then run either:</span></span>

* <span data-ttu-id="2213d-136">**Dtui.exe**：此工具的圖形化介面版本</span><span class="sxs-lookup"><span data-stu-id="2213d-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="2213d-137">**Dt.exe**：此工具的命令列版本</span><span class="sxs-lookup"><span data-stu-id="2213d-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="2213d-138">匯入資料</span><span class="sxs-lookup"><span data-stu-id="2213d-138">Import data</span></span>

<span data-ttu-id="2213d-139">一旦已安裝此工具之後，就可以匯入您的資料。</span><span class="sxs-lookup"><span data-stu-id="2213d-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="2213d-140">您要匯入的資料類型為何？</span><span class="sxs-lookup"><span data-stu-id="2213d-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="2213d-141">JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="2213d-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="2213d-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="2213d-143">MongoDB 匯出檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="2213d-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="2213d-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="2213d-145">CSV 檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="2213d-146">Azure 表格儲存體</span><span class="sxs-lookup"><span data-stu-id="2213d-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="2213d-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="2213d-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="2213d-148">Blob</span><span class="sxs-lookup"><span data-stu-id="2213d-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="2213d-149">Azure Cosmos DB 集合</span><span class="sxs-lookup"><span data-stu-id="2213d-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="2213d-150">HBase</span><span class="sxs-lookup"><span data-stu-id="2213d-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="2213d-151">Azure Cosmos DB 大量匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="2213d-152">Azure Cosmos DB 循序記錄匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="2213d-153"><a id="JSON"></a>匯入 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="2213d-154">JSON 檔案來源匯入工具選項可讓您匯入一或多個單一文件 JSON 檔案或包含 JSON 文件陣列的每個 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="2213d-155">新增包含要匯入之 JSON 檔案的資料夾時，您可以選擇是否要以遞迴方式搜尋子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![JSON 檔案來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/jsonsource.png)

<span data-ttu-id="2213d-157">以下是匯入 JSON 檔案的一些命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="2213d-158"><a id="MongoDB"></a>從 MongoDB 匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2213d-159">如果您要匯入到具有 MongoDB 支援的 Azure Cosmos DB 帳戶，請遵循這些[指示](mongodb-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="2213d-160">MongoDB 來源匯入工具選項可讓您從個別的 MongoDB 集合匯入，並使用查詢來選擇性地篩選文件，及/或使用投影來修改文件結構。</span><span class="sxs-lookup"><span data-stu-id="2213d-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![MongoDB 來源選項的螢幕擷取畫面](./media/import-data/mongodbsource.png)

<span data-ttu-id="2213d-162">連接字串會採用標準的 MongoDB 格式：</span><span class="sxs-lookup"><span data-stu-id="2213d-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="2213d-163">若要確定可以存取連接字串欄位中指定的 MongoDB 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-164">輸入要匯出資料的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="2213d-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="2213d-165">您可以選擇性地對這兩個篩選器指定或提供檔案進行查詢 (例如 {pop: {$gt:5000}} ) 及/或投射 (例如 {loc:0} )，並使資料適合匯入作業。</span><span class="sxs-lookup"><span data-stu-id="2213d-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="2213d-166">以下是從 MongoDB 匯入的一些命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="2213d-167"><a id="MongoDBExport"></a>匯入 MongoDB 匯出檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2213d-168">如果您要匯入具有 MongoDB 支援的 Azure Cosmos DB 帳戶中，請遵循這些[指示](mongodb-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="2213d-169">MongoDB 匯出 JSON 檔案來源匯入工具選項可讓您匯入從 mongoexport 公用程式產生的一或多個 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![MongoDB 匯出來源選項的螢幕擷取畫面](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="2213d-171">新增包含要匯入之 MongoDB 匯出 JSON 檔案的資料夾，您可以選擇是否要以遞迴方式搜尋子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="2213d-172">以下是從 MongoDB 匯出 JSON 檔案匯入的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="2213d-173"><a id="SQL"></a>從 SQL Server 匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="2213d-174">SQL 來源匯入工具選項可讓您從個別的 SQL Server 資料庫匯入，並使用查詢來選擇性地篩選要匯入的記錄。</span><span class="sxs-lookup"><span data-stu-id="2213d-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="2213d-175">此外，您可以藉由指定巢狀分隔符號 (稍後將有更詳細的說明) 來修改文件結構。</span><span class="sxs-lookup"><span data-stu-id="2213d-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![SQL 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/sqlexportsource.png)

<span data-ttu-id="2213d-177">連接字串的格式會採用標準的 SQL 連接字串格式。</span><span class="sxs-lookup"><span data-stu-id="2213d-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="2213d-178">若要確定可以存取連接字串欄位中指定的 SQL Server 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-179">巢狀分隔符號屬性可用來在匯入期間建立階層式關聯性 (子文件)。</span><span class="sxs-lookup"><span data-stu-id="2213d-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="2213d-180">請考慮下列 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="2213d-180">Consider the following SQL query:</span></span>

<bpt id="p1">*</bpt>select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'<ept id="p1">*</ept>

<span data-ttu-id="2213d-182">它會傳回下列 (部分) 結果：</span><span class="sxs-lookup"><span data-stu-id="2213d-182">Which returns the following (partial) results:</span></span>

![SQL 查詢結果的螢幕擷取畫面](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="2213d-184">注意別名，例如 Address.AddressType 和 Address.Location.StateProvinceName。</span><span class="sxs-lookup"><span data-stu-id="2213d-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="2213d-185">藉由指定巢狀分隔符號 ‘.’，匯入工具會在匯入期間建立 Address 和 Address.Location 子文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="2213d-186">在 Azure Cosmos DB 中產生的文件範例如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="2213d-187">{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }</span><span class="sxs-lookup"><span data-stu-id="2213d-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="2213d-188">以下是從 SQL Server 匯入的一些命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="2213d-189"><a id="CSV"></a>匯入 CSV 檔案並將 CSV 轉換成 JSON</span><span class="sxs-lookup"><span data-stu-id="2213d-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="2213d-190">CSV 檔案來源匯入工具選項可讓您匯入一或多個 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="2213d-191">新增包含要匯入之 CSV 檔案的資料夾時，您可以選擇是否要以遞迴方式搜尋子資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![CSV 來源選項的螢幕擷取畫面 - CSV 轉換成 JSON](media/import-data/csvsource.png)

<span data-ttu-id="2213d-193">與 SQL 來源類似，巢狀分隔符號屬性可用來在匯入期間建立階層式關聯性 (子文件)。</span><span class="sxs-lookup"><span data-stu-id="2213d-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="2213d-194">請考慮下列 CSV 標頭資料列和資料資料列：</span><span class="sxs-lookup"><span data-stu-id="2213d-194">Consider the following CSV header row and data rows:</span></span>

![CSV 範例記錄的螢幕擷取畫面 - CSV 轉換成 JSON](./media/import-data/csvsample.png)

<span data-ttu-id="2213d-196">注意別名，例如 DomainInfo.Domain_Name 和 RedirectInfo.Redirecting。</span><span class="sxs-lookup"><span data-stu-id="2213d-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="2213d-197">藉由指定巢狀分隔符號 ‘.’，匯入工具將會在匯入期間建立 DomainInfo 和 RedirectInfo 子文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="2213d-198">在 Azure Cosmos DB 中產生的文件範例如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="2213d-199">{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }</span><span class="sxs-lookup"><span data-stu-id="2213d-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="2213d-200">匯入工具將嘗試推斷 CSV 檔案中不具引號之值的類型資訊 (加上引號的值永遠會被視為字串)。</span><span class="sxs-lookup"><span data-stu-id="2213d-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="2213d-201">系統會依照下列順序識別類型：數字、日期時間、布林值。</span><span class="sxs-lookup"><span data-stu-id="2213d-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="2213d-202">下面提供兩個其他有關 CSV 匯入的注意事項：</span><span class="sxs-lookup"><span data-stu-id="2213d-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="2213d-203">根據預設，不具引號的值一律會針對定位點和空格進行修剪，而具有引號的值則會以原樣方式加以保留。</span><span class="sxs-lookup"><span data-stu-id="2213d-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="2213d-204">您可以使用 [修剪具有引號的值] 核取方塊或 /s.TrimQuoted 命令列選項，來覆寫這個行為。</span><span class="sxs-lookup"><span data-stu-id="2213d-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="2213d-205">根據預設，不具引號的 Null 會被視為 Null 值。</span><span class="sxs-lookup"><span data-stu-id="2213d-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="2213d-206">您可以使用 [將不具引號的 NULL 視為字串] 核取方塊或 /s.NoUnquotedNulls 命令列選項，來覆寫這個行為 (例如，將不具引號的 Null 視為 “null” 字串)。</span><span class="sxs-lookup"><span data-stu-id="2213d-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="2213d-207">以下是 CSV 匯入的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="2213d-208"><a id="AzureTableSource"></a>從 Azure 資料表儲存體匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="2213d-209">Azure 資料表儲存體來源匯入工具選項可讓您從個別的 Azure 資料表儲存體資料表匯入，並選擇性地篩選要匯入的資料表實體。</span><span class="sxs-lookup"><span data-stu-id="2213d-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="2213d-210">請注意，您無法使用資料移轉工具，將 Azure 資料表儲存體資料匯入到 Azure Cosmos DB 來與資料表 API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="2213d-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="2213d-211">目前僅支援匯入到 Azure Cosmos DB 來與 DocumentDB API 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="2213d-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Azure 資料表儲存體來源選項的螢幕擷取畫面](./media/import-data/azuretablesource.png)

<span data-ttu-id="2213d-213">Azure 資料表儲存體連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="2213d-214">若要確定可以存取連接字串欄位中指定的 Azure 資料表儲存體執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-215">輸入要匯出資料的 Azure 資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="2213d-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="2213d-216">您可以選擇性地指定 [篩選器](https://msdn.microsoft.com/library/azure/ff683669.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2213d-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="2213d-217">Azure 資料表儲存體來源匯入工具選項具有下列其他選項：</span><span class="sxs-lookup"><span data-stu-id="2213d-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="2213d-218">包含內部欄位</span><span class="sxs-lookup"><span data-stu-id="2213d-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="2213d-219">全部 - 包括所有內部欄位 (PartitionKey、RowKey 和 Timestamp)</span><span class="sxs-lookup"><span data-stu-id="2213d-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="2213d-220">無 - 排除所有內部欄位</span><span class="sxs-lookup"><span data-stu-id="2213d-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="2213d-221">RowKey - 僅包含 RowKey 欄位</span><span class="sxs-lookup"><span data-stu-id="2213d-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="2213d-222">選取資料行</span><span class="sxs-lookup"><span data-stu-id="2213d-222">Select Columns</span></span>
   1. <span data-ttu-id="2213d-223">Azure 資料表儲存體篩選器不支援投影。</span><span class="sxs-lookup"><span data-stu-id="2213d-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="2213d-224">如果您只想匯入特定的 Azure 資料表實體屬性，請將它們加入 [選取資料行] 清單。</span><span class="sxs-lookup"><span data-stu-id="2213d-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="2213d-225">其他所有實體屬性都會被忽略。</span><span class="sxs-lookup"><span data-stu-id="2213d-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="2213d-226">以下是從 Azure 資料表儲存體匯入的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="2213d-227"><a id="DynamoDBSource"></a>從 Amazon DynamoDB 匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="2213d-228">Amazon DynamoDB 來源匯入工具選項可讓您從個別的 Amazon DynamoDB 資料表匯入，並選擇性地篩選要匯入的實體。</span><span class="sxs-lookup"><span data-stu-id="2213d-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="2213d-229">會提供數個範本，讓設定匯入盡量簡化。</span><span class="sxs-lookup"><span data-stu-id="2213d-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Amazon DynamoDB 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="2213d-232">Amazon DynamoDB 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="2213d-233">若要確定可以存取連接字串欄位中指定的 Amazon DynamoDB 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-234">以下是從 Amazon DynamoDB 匯入的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="2213d-235"><a id="BlobImport"></a>從 Azure Blob 儲存體匯入檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="2213d-236">JSON 檔案、MongoDB 匯出檔案和 CSV 檔案來源匯入工具選項可讓您從 Azure Blob 儲存體匯入一或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="2213d-237">指定 Blob 容器 URL 和帳戶金鑰之後，只需提供規則運算式來選取要匯入的檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Blob 檔案來源選項的螢幕擷取畫面](./media/import-data/blobsource.png)

<span data-ttu-id="2213d-239">以下是從 Azure Blob 儲存體匯入 JSON 檔案的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="2213d-240"><a id="DocumentDBSource"></a>若要從 Azure Cosmos DB DocumentDB API 集合匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="2213d-241">Azure Cosmos DB 來源匯入工具選項可讓您從一或多個 Azure Cosmos DB 集合匯入資料，並選擇性地使用查詢來篩選文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Azure Cosmos DB 來源選項的螢幕擷取畫面](./media/import-data/documentdbsource.png)

<span data-ttu-id="2213d-243">Azure Cosmos DB 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="2213d-244">就像[如何管理 Azure Cosmos DB 帳戶](manage-account.md)中所述，可從 Azure 入口網站的 [金鑰] 刀鋒視窗中擷取 Azure Cosmos DB 帳戶的連接字串，但必須以下列格式將資料庫的名稱附加至連接字串：</span><span class="sxs-lookup"><span data-stu-id="2213d-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="2213d-245">若要確定可以存取連接字串欄位中指定的 Azure Cosmos DB 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-246">若要從單一 Azure Cosmos DB 集合匯入，請輸入要從中匯入資料的來源集合名稱。</span><span class="sxs-lookup"><span data-stu-id="2213d-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="2213d-247">若要從多個 Azure Cosmos DB 集合匯入，可提供規則運算式來比對一或多個集合名稱 (例如 collection01 | collection02 | collection03)。</span><span class="sxs-lookup"><span data-stu-id="2213d-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="2213d-248">您可以選擇性地對這兩個篩選器指定或提供檔案進行查詢，並使資料適合匯入作業。</span><span class="sxs-lookup"><span data-stu-id="2213d-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="2213d-249">因為集合欄位接受規則運算式，所以，若您要從其名稱包含規則運算式字元的單一集合進行匯入，則必須對應地將那些字元逸出。</span><span class="sxs-lookup"><span data-stu-id="2213d-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="2213d-250">Azure Cosmos DB 來源匯入工具選項具有下列進階選項：</span><span class="sxs-lookup"><span data-stu-id="2213d-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="2213d-251">包括內部欄位：指定匯出中是否包含 Azure Cosmos DB 文件系統屬性 (例如 _rid、_ts)。</span><span class="sxs-lookup"><span data-stu-id="2213d-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="2213d-252">失敗時的重試次數：指定與 Azure Cosmos DB 的連接發生暫時性失敗 (例如網路連接中斷) 時的重試次數。</span><span class="sxs-lookup"><span data-stu-id="2213d-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="2213d-253">重試間隔：指定與 Azure Cosmos DB 的連接發生暫時性失敗 (例如網路連接中斷) 時兩次重試之間要等候的時間。</span><span class="sxs-lookup"><span data-stu-id="2213d-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="2213d-254">連線模式：指定要與 Azure Cosmos DB 搭配使用的連線模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="2213d-255">可用的選項包括：DirectTcp、DirectHttps 和閘道器。</span><span class="sxs-lookup"><span data-stu-id="2213d-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="2213d-256">直接連線模式會比較快，但閘道器模式比較支援防火牆，因為它只會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="2213d-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 來源進階選項的螢幕擷取畫面](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="2213d-258">匯入工具會預設 DirectTcp 連線模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="2213d-259">如果您遇到防火牆問題，請切換到閘道器連線模式，因為它只需要連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="2213d-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="2213d-260">以下是從 Azure Cosmos DB 匯入的一些命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="2213d-261">Azure Cosmos DB 資料匯入工具也支援從 [Azure Cosmos DB 模擬器](local-emulator.md)匯入資料。</span><span class="sxs-lookup"><span data-stu-id="2213d-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="2213d-262">從本機模擬器匯入資料時，請將端點設定為 `https://localhost:<port>`。</span><span class="sxs-lookup"><span data-stu-id="2213d-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="2213d-263"><a id="HBaseSource"></a>從 HBase 匯入</span><span class="sxs-lookup"><span data-stu-id="2213d-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="2213d-264">HBase 來源匯入工具選項可讓您從 HBase 資料表匯入資料，並選擇性地篩選資料。</span><span class="sxs-lookup"><span data-stu-id="2213d-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="2213d-265">會提供數個範本，讓設定匯入盡量簡化。</span><span class="sxs-lookup"><span data-stu-id="2213d-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![HBase 檔案來源選項的螢幕擷取畫面](./media/import-data/hbasesource1.png)

![HBase 檔案來源選項的螢幕擷取畫面](./media/import-data/hbasesource2.png)

<span data-ttu-id="2213d-268">HBase Stargate 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="2213d-269">若要確定可以存取連接字串欄位中指定的 HBase 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-270">以下是從 HBase 匯入的命令列範例：</span><span class="sxs-lookup"><span data-stu-id="2213d-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="2213d-271"><a id="DocumentDBBulkTarget"></a>匯入 DocumentDB API 中 (大量匯入)</span><span class="sxs-lookup"><span data-stu-id="2213d-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="2213d-272">為了提高效率，Azure Cosmos DB 大量匯入工具可讓您使用 Azure Cosmos DB 預存程序，從任何可用的來源選項匯入。</span><span class="sxs-lookup"><span data-stu-id="2213d-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="2213d-273">此工具支援匯入到一個單一分割的 Azure Cosmos DB 集合，以及跨多個單一分割 Azure Cosmos DB 集合分割資料的分區化匯入。</span><span class="sxs-lookup"><span data-stu-id="2213d-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="2213d-274">如需分割資料的詳細資訊，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="2213d-275">此工具將建立並執行預存程序，然後從目標集合中將它刪除。</span><span class="sxs-lookup"><span data-stu-id="2213d-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Azure Cosmos DB 大量選項的螢幕擷取畫面](./media/import-data/documentdbbulk.png)

<span data-ttu-id="2213d-277">Azure Cosmos DB 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="2213d-278">就像[如何管理 Azure Cosmos DB 帳戶](manage-account.md)中所述，可從 Azure 入口網站的 [金鑰] 刀鋒視窗中擷取 Azure Cosmos DB 帳戶的連接字串，但必須以下列格式將資料庫的名稱附加至連接字串：</span><span class="sxs-lookup"><span data-stu-id="2213d-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="2213d-279">若要確定可以存取連接字串欄位中指定的 Azure Cosmos DB 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-280">若要匯入到單一集合，請輸入要匯入資料的目標集合名稱，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2213d-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="2213d-281">若要匯入到多個集合，請分別輸入每個集合的名稱，或使用下列語法來指定多個集合：collection_prefix[開始索引 - 結束索引]。</span><span class="sxs-lookup"><span data-stu-id="2213d-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="2213d-282">透過上述語法指定多個集合時，請記住下列事項：</span><span class="sxs-lookup"><span data-stu-id="2213d-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="2213d-283">僅支援整數範圍的名稱模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="2213d-284">例如，指定 collection[0-3] 將產生下列集合：collection0、collection1、collection2、collection3。</span><span class="sxs-lookup"><span data-stu-id="2213d-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="2213d-285">您可以使用縮寫的語法：collection[3] 將發出一組與步驟 1 中所述相同的集合。</span><span class="sxs-lookup"><span data-stu-id="2213d-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="2213d-286">您可以提供一個以上的替代項目。</span><span class="sxs-lookup"><span data-stu-id="2213d-286">More than one substitution can be provided.</span></span> <span data-ttu-id="2213d-287">例如，collection[0-1] [0-9] 將產生 20 個開頭為零的集合名稱 (collection01、..02、..03)。</span><span class="sxs-lookup"><span data-stu-id="2213d-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="2213d-288">指定集合名稱之後，請選擇所需的集合輸送量 (400 RU 到 10,000 RU)。</span><span class="sxs-lookup"><span data-stu-id="2213d-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="2213d-289">為了達到最佳的匯入效能，請選擇較高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="2213d-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="2213d-290">如需效能層級的詳細資訊，請參閱 [Azure Cosmos DB 中的效能層級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2213d-291">效能輸送量設定僅適用於建立集合。</span><span class="sxs-lookup"><span data-stu-id="2213d-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="2213d-292">如果指定的集合已經存在，將不會修改其輸送量。</span><span class="sxs-lookup"><span data-stu-id="2213d-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="2213d-293">匯入到多個集合時，匯入工具支援以雜湊為基礎的分區化。</span><span class="sxs-lookup"><span data-stu-id="2213d-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="2213d-294">在此案例中，指定您想要用來做為資料分割索引鍵的文件屬性 (如果資料分割索引鍵是空白的，文件就會跨目標集合隨機進行分區化)。</span><span class="sxs-lookup"><span data-stu-id="2213d-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="2213d-295">您可以選擇性地指定在匯入期間，匯入來源中的哪些欄位應該做為 Azure Cosmos DB 文件識別碼屬性使用 (請注意，如果文件不包含這個屬性，則匯入工具將產生 GUID 做為識別碼屬性值)。</span><span class="sxs-lookup"><span data-stu-id="2213d-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="2213d-296">匯入期間有數個可用的進階選項。</span><span class="sxs-lookup"><span data-stu-id="2213d-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="2213d-297">首先，雖然此工具包含預設的大量匯入預存程序 (BulkInsert.js)，但您可以選擇指定自己的匯入預存程序：</span><span class="sxs-lookup"><span data-stu-id="2213d-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Azure Cosmos DB 大量插入 sproc 選項的螢幕擷取畫面](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="2213d-299">此外，匯入日期類型時 (例如從 SQL Server 或 MongoDB)，有三種匯入選項可供選擇：</span><span class="sxs-lookup"><span data-stu-id="2213d-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB 日期時間匯入選項的螢幕擷取畫面](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="2213d-301">字串：保存為字串值</span><span class="sxs-lookup"><span data-stu-id="2213d-301">String: Persist as a string value</span></span>
* <span data-ttu-id="2213d-302">Epoch：保存為 Epoch 數值</span><span class="sxs-lookup"><span data-stu-id="2213d-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="2213d-303">兩者：保存字串和 Epoch 數值。</span><span class="sxs-lookup"><span data-stu-id="2213d-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="2213d-304">這個選項會建立子文件，例如："date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="2213d-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="2213d-305">Azure Cosmos DB 大量匯入工具含有下列其他進階選項：</span><span class="sxs-lookup"><span data-stu-id="2213d-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="2213d-306">批次大小：此工具會將批次大小預設為 50。</span><span class="sxs-lookup"><span data-stu-id="2213d-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="2213d-307">如果要匯入很大的文件，請考慮降低批次大小。</span><span class="sxs-lookup"><span data-stu-id="2213d-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="2213d-308">相反地，如果要匯入很小的文件，請考慮提高批次大小。</span><span class="sxs-lookup"><span data-stu-id="2213d-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="2213d-309">指令碼大小上限 (位元組)：此工具預設將指令碼大小上限設為 512 KB</span><span class="sxs-lookup"><span data-stu-id="2213d-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="2213d-310">停用自動化識別碼產生作業：如果要匯入的每個文件都包含識別碼欄位，則選取此選項可以提升效能。</span><span class="sxs-lookup"><span data-stu-id="2213d-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="2213d-311">遺漏唯一識別碼欄位的文件將不會被匯入。</span><span class="sxs-lookup"><span data-stu-id="2213d-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="2213d-312">更新現有的文件：此工具預設在發生識別碼衝突時不會取代現有的文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="2213d-313">如果選取此選項，將會允許在識別碼相符時覆寫現有的文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="2213d-314">對於會更新現有文件的已排定資料移轉來說，這項功能相當有用。</span><span class="sxs-lookup"><span data-stu-id="2213d-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="2213d-315">失敗時的重試次數：指定與 Azure Cosmos DB 的連接發生暫時性失敗 (例如網路連接中斷) 時的重試次數。</span><span class="sxs-lookup"><span data-stu-id="2213d-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="2213d-316">重試間隔：指定與 Azure Cosmos DB 的連接發生暫時性失敗 (例如網路連接中斷) 時兩次重試之間要等候的時間。</span><span class="sxs-lookup"><span data-stu-id="2213d-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="2213d-317">連線模式：指定要與 Azure Cosmos DB 搭配使用的連線模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="2213d-318">可用的選項包括：DirectTcp、DirectHttps 和閘道器。</span><span class="sxs-lookup"><span data-stu-id="2213d-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="2213d-319">直接連線模式會比較快，但閘道器模式比較支援防火牆，因為它只會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="2213d-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 大量匯入進階選項的螢幕擷取畫面](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="2213d-321">匯入工具會預設 DirectTcp 連線模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="2213d-322">如果您遇到防火牆問題，請切換到閘道器連線模式，因為它只需要連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="2213d-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="2213d-323"><a id="DocumentDBSeqTarget"></a>匯入 DocumentDB API 中 (循序記錄匯入)</span><span class="sxs-lookup"><span data-stu-id="2213d-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="2213d-324">Azure Cosmos DB 循序記錄匯入工具可讓您從任何可用的來源選項逐筆匯入記錄。</span><span class="sxs-lookup"><span data-stu-id="2213d-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="2213d-325">如果您打算匯入至已達到預存程序配額的現有集合，您可以選擇此選項。</span><span class="sxs-lookup"><span data-stu-id="2213d-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="2213d-326">此工具支援匯入到單一 (單一分割區和多重分割區兩者) 的 Azure Cosmos DB 集合，以及跨多個單一分割區和/或多重分割區 Azure Cosmos DB 集合分割資料的分區化匯入。</span><span class="sxs-lookup"><span data-stu-id="2213d-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="2213d-327">如需分割資料的詳細資訊，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Azure Cosmos DB 循序記錄匯入選項的螢幕擷取畫面](./media/import-data/documentdbsequential.png)

<span data-ttu-id="2213d-329">Azure Cosmos DB 連接字串的格式如下：</span><span class="sxs-lookup"><span data-stu-id="2213d-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="2213d-330">就像[如何管理 Azure Cosmos DB 帳戶](manage-account.md)中所述，可從 Azure 入口網站的 [金鑰] 刀鋒視窗中擷取 Azure Cosmos DB 帳戶的連接字串，但必須以下列格式將資料庫的名稱附加至連接字串：</span><span class="sxs-lookup"><span data-stu-id="2213d-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="2213d-331">若要確定可以存取連接字串欄位中指定的 Azure Cosmos DB 執行個體，請使用 Verify 命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="2213d-332">若要匯入到單一集合，請輸入要匯入資料的目標集合名稱，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2213d-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="2213d-333">若要匯入到多個集合，請分別輸入每個集合的名稱，或使用下列語法來指定多個集合：collection_prefix[開始索引 - 結束索引]。</span><span class="sxs-lookup"><span data-stu-id="2213d-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="2213d-334">透過上述語法指定多個集合時，請記住下列事項：</span><span class="sxs-lookup"><span data-stu-id="2213d-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="2213d-335">僅支援整數範圍的名稱模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="2213d-336">例如，指定 collection[0-3] 將產生下列集合：collection0、collection1、collection2、collection3。</span><span class="sxs-lookup"><span data-stu-id="2213d-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="2213d-337">您可以使用縮寫的語法：collection[3] 將發出一組與步驟 1 中所述相同的集合。</span><span class="sxs-lookup"><span data-stu-id="2213d-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="2213d-338">您可以提供一個以上的替代項目。</span><span class="sxs-lookup"><span data-stu-id="2213d-338">More than one substitution can be provided.</span></span> <span data-ttu-id="2213d-339">例如，collection[0-1] [0-9] 將產生 20 個開頭為零的集合名稱 (collection01、..02、..03)。</span><span class="sxs-lookup"><span data-stu-id="2213d-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="2213d-340">指定集合名稱之後，請選擇所需的集合輸送量 (400 RU 到 250,000 RU)。</span><span class="sxs-lookup"><span data-stu-id="2213d-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="2213d-341">為了達到最佳的匯入效能，請選擇較高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="2213d-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="2213d-342">如需效能層級的詳細資訊，請參閱 [Azure Cosmos DB 中的效能層級](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="2213d-343">任何輸送量 >10000 RU 的集合匯入作業都需要資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2213d-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="2213d-344">如果您選擇擁有 250,000 以上的 RU，您將需要在入口網站中提出要求來提升您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2213d-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="2213d-345">輸送量設定僅適用於建立集合。</span><span class="sxs-lookup"><span data-stu-id="2213d-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="2213d-346">如果指定的集合已經存在，將不會修改其輸送量。</span><span class="sxs-lookup"><span data-stu-id="2213d-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="2213d-347">匯入到多個集合時，匯入工具支援以雜湊為基礎的分區化。</span><span class="sxs-lookup"><span data-stu-id="2213d-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="2213d-348">在此案例中，指定您想要用來做為資料分割索引鍵的文件屬性 (如果資料分割索引鍵是空白的，文件就會跨目標集合隨機進行分區化)。</span><span class="sxs-lookup"><span data-stu-id="2213d-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="2213d-349">您可以選擇性地指定在匯入期間，匯入來源中的哪些欄位應該做為 Azure Cosmos DB 文件識別碼屬性使用 (請注意，如果文件不包含這個屬性，則匯入工具將產生 GUID 做為識別碼屬性值)。</span><span class="sxs-lookup"><span data-stu-id="2213d-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="2213d-350">匯入期間有數個可用的進階選項。</span><span class="sxs-lookup"><span data-stu-id="2213d-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="2213d-351">首先，匯入日期類型時 (例如從 SQL Server 或 MongoDB)，有三種匯入選項可供選擇：</span><span class="sxs-lookup"><span data-stu-id="2213d-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Azure Cosmos DB 日期時間匯入選項的螢幕擷取畫面](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="2213d-353">字串：保存為字串值</span><span class="sxs-lookup"><span data-stu-id="2213d-353">String: Persist as a string value</span></span>
* <span data-ttu-id="2213d-354">Epoch：保存為 Epoch 數值</span><span class="sxs-lookup"><span data-stu-id="2213d-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="2213d-355">兩者：保存字串和 Epoch 數值。</span><span class="sxs-lookup"><span data-stu-id="2213d-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="2213d-356">這個選項會建立子文件，例如："date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="2213d-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="2213d-357">Azure Cosmos DB 循序記錄匯入工具含有下列其他進階選項：</span><span class="sxs-lookup"><span data-stu-id="2213d-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="2213d-358">平行要求數目：此工具會預設為 2 個平行要求。</span><span class="sxs-lookup"><span data-stu-id="2213d-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="2213d-359">如果要匯入很小的文件，請考慮提高平行要求數目。</span><span class="sxs-lookup"><span data-stu-id="2213d-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="2213d-360">請注意，如果這個數字提高太多，則匯入可能會發生節流。</span><span class="sxs-lookup"><span data-stu-id="2213d-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="2213d-361">停用自動化識別碼產生作業：如果要匯入的每個文件都包含識別碼欄位，則選取此選項可以提升效能。</span><span class="sxs-lookup"><span data-stu-id="2213d-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="2213d-362">遺漏唯一識別碼欄位的文件將不會被匯入。</span><span class="sxs-lookup"><span data-stu-id="2213d-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="2213d-363">更新現有的文件：此工具預設在發生識別碼衝突時不會取代現有的文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="2213d-364">如果選取此選項，將會允許在識別碼相符時覆寫現有的文件。</span><span class="sxs-lookup"><span data-stu-id="2213d-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="2213d-365">對於會更新現有文件的已排定資料移轉來說，這項功能相當有用。</span><span class="sxs-lookup"><span data-stu-id="2213d-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="2213d-366">失敗時的重試次數：指定與 Azure Cosmos DB 的連接發生暫時性失敗 (例如網路連接中斷) 時的重試次數。</span><span class="sxs-lookup"><span data-stu-id="2213d-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="2213d-367">重試間隔：指定與 Azure Cosmos DB 的連接發生暫時性失敗 (例如網路連接中斷) 時兩次重試之間要等候的時間。</span><span class="sxs-lookup"><span data-stu-id="2213d-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="2213d-368">連線模式：指定要與 Azure Cosmos DB 搭配使用的連線模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="2213d-369">可用的選項包括：DirectTcp、DirectHttps 和閘道器。</span><span class="sxs-lookup"><span data-stu-id="2213d-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="2213d-370">直接連線模式會比較快，但閘道器模式比較支援防火牆，因為它只會使用連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="2213d-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Azure Cosmos DB 循序記錄匯入進階選項的螢幕擷取畫面](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="2213d-372">匯入工具會預設 DirectTcp 連線模式。</span><span class="sxs-lookup"><span data-stu-id="2213d-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="2213d-373">如果您遇到防火牆問題，請切換到閘道器連線模式，因為它只需要連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="2213d-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="2213d-374"><a id="IndexingPolicy"></a>建立 Azure Cosmos DB 集合時指定編製索引原則</span><span class="sxs-lookup"><span data-stu-id="2213d-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="2213d-375">當您允許移轉工具在匯入期間建立集合時，您可以指定集合的索引編製原則。</span><span class="sxs-lookup"><span data-stu-id="2213d-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="2213d-376">在 Azure Cosmos DB 大量匯入和 Azure Cosmos DB 循序記錄選項的進階選項區段中，瀏覽至 [編製索引原則] 區段。</span><span class="sxs-lookup"><span data-stu-id="2213d-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Azure Cosmos DB 編製索引原則進階選項的螢幕擷取畫面](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="2213d-378">使用索引編製原則進階選項，您可以選取索引編製原則檔案，以手動方式輸入索引編製原則，或從一組預設範本中選取 (以滑鼠右鍵按一下索引編製原則文字方塊)。</span><span class="sxs-lookup"><span data-stu-id="2213d-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="2213d-379">此工具提供的原則範本是：</span><span class="sxs-lookup"><span data-stu-id="2213d-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="2213d-380">預設值。</span><span class="sxs-lookup"><span data-stu-id="2213d-380">Default.</span></span> <span data-ttu-id="2213d-381">當您使用 ORDER BY、範圍和數字的相等查詢針對字串進行相等查詢時，這是最佳的原則。</span><span class="sxs-lookup"><span data-stu-id="2213d-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="2213d-382">這個原則的索引儲存空間負擔比範圍低。</span><span class="sxs-lookup"><span data-stu-id="2213d-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="2213d-383">範圍。</span><span class="sxs-lookup"><span data-stu-id="2213d-383">Range.</span></span> <span data-ttu-id="2213d-384">當您使用 ORDER BY、範圍以及數字和字串的相等查詢時，這是最佳的原則。</span><span class="sxs-lookup"><span data-stu-id="2213d-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="2213d-385">這個原則的索引儲存空間負擔比預設或雜湊高。</span><span class="sxs-lookup"><span data-stu-id="2213d-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Azure Cosmos DB 編製索引原則進階選項的螢幕擷取畫面](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="2213d-387">如果未指定索引編製原則，將會套用預設原則。</span><span class="sxs-lookup"><span data-stu-id="2213d-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="2213d-388">如需編製索引原則的詳細資訊，請參閱 [Azure Cosmos DB 編製索引原則](indexing-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="2213d-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="2213d-389">匯出至 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="2213d-389">Export to JSON file</span></span>
<span data-ttu-id="2213d-390">Azure Cosmos DB JSON 匯出工具可讓您將任何可用的來源選項匯出至包含 JSON 文件陣列的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="2213d-391">此工具將會為您處理匯出作業，或者您可以選擇檢視產生的移轉命令，然後自己執行命令。</span><span class="sxs-lookup"><span data-stu-id="2213d-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="2213d-392">產生的 JSON 檔案可能會儲存在本機或 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="2213d-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Azure Cosmos DB JSON 本機檔案匯出選項的螢幕擷取畫面](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob 儲存體匯出選項的螢幕擷取畫面](./media/import-data/jsontarget2.png)

<span data-ttu-id="2213d-395">您可以選擇性地選擇美化產生的 JSON，這會增加產生文件的大小，但會使內容更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="2213d-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="2213d-396">進階組態</span><span class="sxs-lookup"><span data-stu-id="2213d-396">Advanced configuration</span></span>
<span data-ttu-id="2213d-397">在 [進階組態] 畫面中，指定您想要寫入所有錯誤的記錄檔位置。</span><span class="sxs-lookup"><span data-stu-id="2213d-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="2213d-398">下列規則會套用到此頁面：</span><span class="sxs-lookup"><span data-stu-id="2213d-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="2213d-399">如果未提供檔案名稱，則會在 [結果] 頁面上傳回所有錯誤。</span><span class="sxs-lookup"><span data-stu-id="2213d-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="2213d-400">如果提供不含目錄的檔案名稱，則會在目前的環境目錄中建立 (或覆寫) 該檔案。</span><span class="sxs-lookup"><span data-stu-id="2213d-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="2213d-401">如果選取了現有的檔案，則將會覆寫該檔案，沒有任何附加選項。</span><span class="sxs-lookup"><span data-stu-id="2213d-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="2213d-402">然後，選擇是要記錄所有錯誤訊息、嚴重錯誤訊息，還是不記錄任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="2213d-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="2213d-403">最後，決定螢幕上傳輸訊息更新其進度的頻率。</span><span class="sxs-lookup"><span data-stu-id="2213d-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="2213d-404">確認匯入設定及檢視命令列</span><span class="sxs-lookup"><span data-stu-id="2213d-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="2213d-405">指定來源資訊、目標資訊與進階組態之後，請檢閱移轉摘要，並選擇性地檢視或複製產生的移轉命令 (複製命令對於自動匯入作業非常有用)：</span><span class="sxs-lookup"><span data-stu-id="2213d-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![摘要畫面的螢幕擷取畫面](./media/import-data/summary.png)
   
    ![摘要畫面的螢幕擷取畫面](./media/import-data/summarycommand.png)
2. <span data-ttu-id="2213d-408">在您滿意來源和目標選項之後，請按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="2213d-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="2213d-409">隨著匯入的處理，已耗用時間、傳送的計數，以及失敗的資訊 (如果您未在 [進階組態] 中提供檔案名稱) 都將隨之更新。</span><span class="sxs-lookup"><span data-stu-id="2213d-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="2213d-410">完成後，您可以匯出結果 (例如處理任何匯入失敗)。</span><span class="sxs-lookup"><span data-stu-id="2213d-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Azure Cosmos DB JSON 匯出選項的螢幕擷取畫面](./media/import-data/viewresults.png)
3. <span data-ttu-id="2213d-412">您也可以啟動新的匯入，您可以保留現有設定 (例如連接字串資訊、來源和目標選擇等)，或重設所有值。</span><span class="sxs-lookup"><span data-stu-id="2213d-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Azure Cosmos DB JSON 匯出選項的螢幕擷取畫面](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="2213d-414">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2213d-414">Next steps</span></span>

<span data-ttu-id="2213d-415">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="2213d-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2213d-416">已安裝資料移轉工具</span><span class="sxs-lookup"><span data-stu-id="2213d-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="2213d-417">已從不同的資料來源匯入資料</span><span class="sxs-lookup"><span data-stu-id="2213d-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="2213d-418">已從 Azure Cosmos DB 匯出到 JSON</span><span class="sxs-lookup"><span data-stu-id="2213d-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="2213d-419">您現在可以繼續進行下一個教學課程，了解如何使用 Azure Cosmos DB 查詢資料。</span><span class="sxs-lookup"><span data-stu-id="2213d-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="2213d-420">如何查詢資料？</span><span class="sxs-lookup"><span data-stu-id="2213d-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
