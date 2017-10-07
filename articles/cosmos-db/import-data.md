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
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>如何針對 Azure Cosmos DB tooimport 資料 hello DocumentDB API 嗎？

本教學課程提供說明如何使用 hello Azure Cosmos DB: DocumentDB API 資料移轉工具，可以從各種來源，包括 JSON 檔案匯入資料 CSV 檔案、 SQL、 MongoDB、 Azure 資料表儲存體，Amazon DynamoDB 和 Azure Cosmos DB DocumentDB集合中的 API 集合使用 Azure Cosmos DB 與 hello DocumentDB API。 hello DocumentDB API，單一資料分割集合 tooa 多個資料分割集合移轉時，可以也使用 hello 資料移轉工具。

當匯入資料到 Azure DB Cosmos 使用 hello DocumentDB API 時，只適用於 hello 資料移轉工具。 在此階段不支援匯入適用於 hello 表格 API 或 Graph API 的資料。 

tooimport hello MongoDB API 搭配使用的資料，請參閱[Azure Cosmos DB: toomigrate 資料如何 hello MongoDB API？](mongodb-migrate.md)。

本教學課程涵蓋 hello 下列工作：

> [!div class="checklist"]
> * 安裝 hello 資料移轉工具
> * 從不同的資料來源匯入資料
> * 從 Azure Cosmos DB tooJSON 匯出

## <a id="Prerequisites"></a>必要條件
之前遵循這篇文章中的 hello 指示，請確定您擁有 hello 安裝下列項目：

* [Microsoft.NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) 或更高版本。

## <a id="Overviewl"></a>Hello 資料移轉工具的概觀
hello 資料移轉工具是開放原始碼解決方案從各種不同的來源，包括匯入資料 tooAzure Cosmos DB:

* JSON 檔案
* MongoDB
* SQL Server
* CSV 檔案
* Azure 資料表儲存體
* Amazon DynamoDB
* HBase
* Azure Cosmos DB 集合

雖然 hello 匯入工具包含圖形化使用者介面 (dtui.exe)，它可以也衍生自 hello 命令列 (dt.exe)。 事實上，設定透過 hello UI 匯入之後沒有選項 toooutput hello 相關聯的命令。 表格式來源資料 (例如 SQL Server 或 CSV 檔案) 可以進行轉換，以致可以在匯入期間建立階層式關聯性 (子文件)。 繼續閱讀更多有關來源選項，每個來源的範例命令列 tooimport toolearn、 目標選項和檢視結果匯入。

## <a id="Install"></a>安裝 hello 資料移轉工具
hello 移轉工具的原始程式碼可在 GitHub 上[這個儲存機制](https://github.com/azure/azure-documentdb-datamigrationtool)而且編譯的版本都可從[Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)。 您可能會編譯 hello 方案或只是下載及擷取您所選擇的 hello 編譯的版本 tooa 目錄。 然後執行：

* **Dtui.exe**: hello 工具的圖形化介面版本
* **Dt.exe**: hello 工具命令列版本

## <a name="import-data"></a>匯入資料

一旦您已安裝 hello 工具，就是時間 tooimport 您的資料。 何種類型的資料是否要 tooimport？

* [JSON 檔案](#JSON)
* [MongoDB](#MongoDB)
* [MongoDB 匯出檔案](#MongoDBExport)
* [SQL Server](#SQL)
* [CSV 檔案](#CSV)
* [Azure 表格儲存體](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource)
* [Blob](#BlobImport)
* [Azure Cosmos DB 集合](#DocumentDBSource)
* [HBase](#HBaseSource)
* [Azure Cosmos DB 大量匯入](#DocumentDBBulkImport)
* [Azure Cosmos DB 循序記錄匯入](#DocumentDSeqTarget)


## <a id="JSON"></a>tooimport JSON 檔案
hello JSON 檔案來源匯入工具選項可讓您 tooimport 其中一個或多個單一文件 JSON 檔案或將 JSON 檔案，其中每個包含 JSON 文件的陣列。 新增包含 JSON 檔案 tooimport 資料夾，您會有 hello 選項以遞迴方式搜尋子資料夾中的檔案。

![JSON 檔案來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/jsonsource.png)

以下是一些命令列範例 tooimport JSON 檔案：

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

## <a id="MongoDB"></a>從 MongoDB tooimport

> [!IMPORTANT]
> 如果您要匯入 Support for MongoDB tooan Azure Cosmos DB 帳戶，請遵循這些[指示](mongodb-migrate.md)。
> 
> 

hello MongoDB 來源匯入工具選項可讓您從個別的 MongoDB 集合 tooimport 並選擇性地篩選使用查詢的文件及/或使用投影來修改 hello 文件結構。  

![MongoDB 來源選項的螢幕擷取畫面](./media/import-data/mongodbsource.png)

hello 連接字串是以標準 MongoDB 格式 hello:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> 使用 hello 確認命令 tooensure hello MongoDB hello 連接字串 欄位中指定的執行個體，可以存取。
> 
> 

輸入 hello hello 匯入資料的集合名稱。 您可能會選擇性地指定，或者提供查詢檔 (例如 {pop: {$gt: 5000}}) 及/或投射 (例如 {loc:0}) tooboth 篩選器和圖形 hello 資料 toobe 匯入。

以下是一些從 MongoDB 的命令列範例 tooimport:

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>tooimport MongoDB 匯出檔案

> [!IMPORTANT]
> 如果您要匯入 support for MongoDB。 tooan Azure Cosmos DB 帳戶，請遵循這些[指示](mongodb-migrate.md)。
> 
> 

hello MongoDB 匯出 JSON 檔案來源匯入工具選項可讓您 tooimport 其中一個或更多的 JSON 檔案產生從 hello mongoexport 公用程式。  

![MongoDB 匯出來源選項的螢幕擷取畫面](./media/import-data/mongodbexportsource.png)

新增包含 MongoDB 匯出 JSON 檔案匯入的資料夾，您會有 hello 選項以遞迴方式搜尋子資料夾中的檔案。

以下是從 MongoDB 匯出的命令列範例 tooimport JSON 檔案：

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>從 SQL Server tooimport
hello SQL 來源匯入工具選項可讓您 tooimport 從個別的 SQL Server 資料庫，並選擇性地篩選 hello 記錄 toobe 匯入使用的查詢。 此外，您可以藉由指定巢狀的分隔符號 （稍後將詳細） 修改 hello 文件結構。  

![SQL 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/sqlexportsource.png)

hello hello 連接字串格式是 hello 標準 SQL 連接字串格式。

> [!NOTE]
> 使用 hello 確認命令 tooensure hello hello 連接字串 欄位中指定的 SQL Server 執行個體，可以存取。
> 
> 

hello 巢狀方式置於 [分隔符號] 屬性匯入期間是使用的 toocreate 階層式關聯性 （子文件）。 請考慮下列 SQL 查詢的 hello:

<bpt id="p1">*</bpt>select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'<ept id="p1">*</ept>

它會傳回下列結果 （部分） 的 hello:

![SQL 查詢結果的螢幕擷取畫面](./media/import-data/sqlqueryresults.png)

請注意 Address.AddressType 等 Address.Location.StateProvinceName hello 別名。 藉由指定的巢狀分隔符號 '。 '、 hello 匯入工具建立位址，並匯入期間 hello Address.Location 子文件。 在 Azure Cosmos DB 中產生的文件範例如下：

{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }

以下是一些命令列範例 tooimport，從 SQL Server:

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>tooimport CSV 檔案和轉換 CSV tooJSON
hello CSV 檔案來源匯入工具選項可讓您 tooimport 一或多個 CSV 檔案。 新增包含匯入 CSV 檔案的資料夾，您會有 hello 選項以遞迴方式搜尋子資料夾中的檔案。

![螢幕擷取畫面的 CSV 來源選項 CSV tooJSON](media/import-data/csvsource.png)

匯入期間，類似 toohello SQL 來源，hello 巢狀分隔符號屬性可能會使用的 toocreate 階層式關聯性 （子文件）。 請考慮下列 CSV 標頭資料列和資料列的 hello:

![螢幕擷取畫面的 CSV 範例記錄 CSV tooJSON](./media/import-data/csvsample.png)

請注意 DomainInfo.Domain_Name 等 RedirectInfo.Redirecting hello 別名。 藉由指定的巢狀分隔符號 '。 ' hello 匯入工具會建立 DomainInfo，匯入期間 hello RedirectInfo 子文件。 在 Azure Cosmos DB 中產生的文件範例如下：

*{"DomainInfo": {"Domain_Name":"ACUS.GOV"、"Domain_Name_Address":"http://www。ACUS.GOV"}，「 美國聯邦代理者 」: 「 系統管理會議的 hello 美國 」、 「 RedirectInfo": {」 重新導向 」:"0"、"Redirect_Destination":""}，"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*

hello 匯入工具會嘗試 tooinfer 類型值的資訊未加引號之 CSV 檔案中 （加上引號的值會一律視為字串）。  Hello 順序中所識別的型別： 數字、 datetime、 布林值。  

有兩個其他項目 toonote 關於 CSV 匯入：

1. 根據預設，不具引號的值一律會針對定位點和空格進行修剪，而具有引號的值則會以原樣方式加以保留。 Hello Trim 加上引號的值核取方塊或 hello /s.TrimQuoted 命令列選項可以覆寫此行為。
2. 根據預設，不具引號的 Null 會被視為 Null 值。 覆寫這個行為 （亦即視為不具引號的 null"null"字串） 以 hello Treat 不加引號的字串核取方塊 hello /s.NoUnquotedNulls 命令列選項或為 NULL。

以下是 CSV 匯入的命令列範例：

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>從 Azure 資料表儲存體 tooimport
hello Azure 資料表儲存體來源匯入工具選項可讓您從個別的 Azure 資料表儲存體資料表 tooimport，並選擇性地篩選 hello 資料表實體 toobe 匯入。 請注意，您不可使用 hello 資料移轉工具 tooimport Azure 資料表儲存體資料到 Azure Cosmos DB hello 表格 API 搭配使用。 目前支援僅匯入 tooAzure Cosmos DB hello DocumentDB API 搭配使用。

![Azure 資料表儲存體來源選項的螢幕擷取畫面](./media/import-data/azuretablesource.png)

hello 的 hello Azure 資料表儲存體連接字串的格式如下：

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> 使用 hello 確認命令 tooensure hello hello 連接字串 欄位中指定的 Azure 資料表儲存體執行個體，可以存取。
> 
> 

輸入 hello 名稱 hello Azure 匯入資料的資料表。 您可以選擇性地指定 [篩選器](https://msdn.microsoft.com/library/azure/ff683669.aspx)。

hello Azure 資料表儲存體來源匯入工具選項具有下列其他選項的 hello:

1. 包含內部欄位
   1. 全部 - 包括所有內部欄位 (PartitionKey、RowKey 和 Timestamp)
   2. 無 - 排除所有內部欄位
   3. RowKey-只包含 hello RowKey 欄位
2. 選取資料行
   1. Azure 資料表儲存體篩選器不支援投影。 如果您想 tooonly 匯入特定 Azure 資料表實體屬性，請將其加入 toohello 選取資料行清單。 其他所有實體屬性都會被忽略。

以下是命令列範例 tooimport 從 Azure 資料表儲存體：

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>從 Amazon DynamoDB tooimport
hello Amazon DynamoDB 來源匯入工具選項可讓您從個別的 Amazon DynamoDB 資料表 tooimport，並選擇性地篩選 hello 實體 toobe 匯入。 會提供數個範本，讓設定匯入盡量簡化。

![Amazon DynamoDB 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/dynamodbsource1.png)

![Amazon DynamoDB 來源選項的螢幕擷取畫面 - 資料庫移轉工具](./media/import-data/dynamodbsource2.png)

hello 的 hello Amazon DynamoDB 連接字串的格式如下：

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> 使用 hello 確認命令 tooensure hello Amazon DynamoDB hello 連接字串 欄位中指定的執行個體，可以存取。
> 
> 

以下是從 Amazon DynamoDB 命令列範例 tooimport:

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>從 Azure Blob 儲存體 tooimport 檔案
hello JSON 檔案、 MongoDB 匯出檔案和 CSV 檔案來源匯入工具選項可讓您 tooimport 從 Azure Blob 儲存體的一或多個檔案。 指定 Blob 容器 URL 和帳戶金鑰之後, 直接提供規則運算式 tooselect hello 檔案 tooimport。

![Blob 檔案來源選項的螢幕擷取畫面](./media/import-data/blobsource.png)

以下是命令列範例 tooimport JSON 檔案從 Azure Blob 儲存體：

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>從 Azure Cosmos DB DocumentDB API 集合 tooimport
hello Azure Cosmos DB 來源匯入工具選項可讓您從一或多個 Azure Cosmos DB 集合 tooimport 資料，並選擇性地篩選使用查詢的文件。  

![Azure Cosmos DB 來源選項的螢幕擷取畫面](./media/import-data/documentdbsource.png)

hello 的 hello Azure Cosmos DB 的連接字串的格式如下：

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

hello Azure Cosmos DB 帳戶連接字串可從擷取的 hello 金鑰刀鋒視窗中的 hello Azure 入口網站中所述[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md)，不過 hello hello 資料庫名稱必須附加 toobe toohellohello 遵循格式中的連接字串：

    Database=<CosmosDB Database>;

> [!NOTE]
> 使用 hello 確認命令 tooensure hello Azure Cosmos DB hello 連接字串 欄位中指定的執行個體，可以存取。
> 
> 

單一 Azure Cosmos DB 集合，從 tooimport 輸入 hello hello 匯入資料的集合名稱。 從多個 Azure Cosmos DB 集合，tooimport 提供規則運算式 toomatch 一或多個集合的名稱 (例如 collection01 | collection02 | collection03)。 您可能會選擇性地指定，或提供的查詢 tooboth 篩選檔圖案和 hello 資料 toobe 匯入。

> [!NOTE]
> 因為 hello 集合欄位接受規則運算式，如果您要匯入從單一集合，其名稱包含規則運算式的字元，然後這些字元必須逸出據此。
> 
> 

hello Azure Cosmos DB 來源匯入工具選項已經 hello 下列進階選項：

1. 包含內部欄位： 指定在 hello tooinclude Azure Cosmos DB 文件系統屬性匯出 (例如 _rid，_ts)。
2. 失敗的重試次數： 指定 tooretry hello 連接 tooAzure Cosmos DB 在暫時性失敗 （例如網路連線中斷） 的 hello 次數。
3. 重試間隔： 指定多久 toowait 之間發生暫時性失敗 （例如網路連線中斷） 的 hello 連接 tooAzure Cosmos DB 重試一次。
4. 連接模式： 指定 hello 連線模式 toouse 搭配 Azure Cosmos DB。 hello 可用的選項是 DirectTcp、 DirectHttps 和閘道。 hello 直接連線模式速度較快，而 hello 閘道模式是多個防火牆易記，因為它只會使用連接埠 443。

![Azure Cosmos DB 來源進階選項的螢幕擷取畫面](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> hello 匯入工具的預設值 tooconnection 模式 DirectTcp。 如果您遇到防火牆問題，請切換 tooconnection 模式閘道，因為它只需要連接埠 443。
> 
> 

以下是一些命令列範例 tooimport，從 Azure Cosmos DB:

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> hello Azure Cosmos DB 的資料匯入的工具也支援匯入的資料從 hello [Azure Cosmos DB 模擬器](local-emulator.md)。 當從本機模擬器，匯入資料，設定 hello 端點太`https://localhost:<port>`。 
> 
> 

## <a id="HBaseSource"></a>從 HBase tooimport
hello HBase 來源匯入工具選項可讓您 tooimport HBase 資料表的資料，並選擇性地篩選 hello 資料。 會提供數個範本，讓設定匯入盡量簡化。

![HBase 檔案來源選項的螢幕擷取畫面](./media/import-data/hbasesource1.png)

![HBase 檔案來源選項的螢幕擷取畫面](./media/import-data/hbasesource2.png)

hello 的 hello HBase Stargate 連接字串的格式如下：

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> 使用 hello 確認命令 tooensure hello HBase hello 連接字串 欄位中指定的執行個體，可以存取。
> 
> 

以下是從 HBase 命令列範例 tooimport:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API （大量匯入）
hello Azure Cosmos DB 大量匯入工具，可讓您從任何 hello 可用的來源選項，請使用 Azure Cosmos DB 預存程序以提升效率 tooimport。 hello 工具支援匯入 tooone 單一分割 Azure Cosmos DB 集合，以及在多個單一資料分割 Azure Cosmos DB 集合分割資料分割的分區化匯入。 如需分割資料的詳細資訊，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。 hello 工具會建立、 執行，然後刪除 hello 目標清查中的 hello 預存程序。  

![Azure Cosmos DB 大量選項的螢幕擷取畫面](./media/import-data/documentdbbulk.png)

hello 的 hello Azure Cosmos DB 的連接字串的格式如下：

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

hello Azure Cosmos DB 帳戶連接字串可從擷取的 hello 金鑰刀鋒視窗中的 hello Azure 入口網站中所述[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md)，不過 hello hello 資料庫名稱必須附加 toobe toohellohello 遵循格式中的連接字串：

    Database=<CosmosDB Database>;

> [!NOTE]
> 使用 hello 確認命令 tooensure hello Azure Cosmos DB hello 連接字串 欄位中指定的執行個體，可以存取。
> 
> 

tooimport tooa 單一集合中，輸入 hello 名稱 hello 集合 toowhich 資料將匯入和按一下 hello [新增] 按鈕。 tooimport toomultiple 集合、 個別輸入每個集合的名稱或使用下列語法 toospecify hello 多個集合： *collection_prefix*[start 索引-結束索引]。 當指定多個集合，透過 hello 上述語法，請記住 hello 下列：

1. 僅支援整數範圍的名稱模式。 比方說，指定集合 [0-3] 將會產生下列集合的 hello: collection0，collection1，collection2，collection3。
2. 您可以使用縮寫的語法：collection[3] 將發出一組與步驟 1 中所述相同的集合。
3. 您可以提供一個以上的替代項目。 例如，collection[0-1] [0-9] 將產生 20 個開頭為零的集合名稱 (collection01、..02、..03)。

一旦 hello 集合名稱已指定，則選擇 hello 的 hello 清查 (400 Ru too10，000 RUs) 所需的輸送量。 為了達到最佳的匯入效能，請選擇較高的輸送量。 如需效能層級的詳細資訊，請參閱 [Azure Cosmos DB 中的效能層級](performance-levels.md)。

> [!NOTE]
> hello 效能輸送量設定僅適用於 toocollection 建立。 如果 hello 指定集合已經存在，將不會修改其輸送量。
> 
> 

當匯入 toomultiple 集合，hello 匯入工具會支援基礎的雜湊分區化。 在此案例中，指定您想 toouse hello 資料分割索引鍵為 hello 文件屬性 （如果空白的資料分割索引鍵，文件將分區化隨機跨 hello 目標集合）。

您可以選擇性地指定 hello 匯入來源中的哪一個欄位應該做為 hello Azure Cosmos DB 文件的 id 屬性期間 hello 匯入 （請注意，如果文件未包含此屬性，則 hello 匯入工具會產生 hello id 屬性值為 GUID）。

匯入期間有數個可用的進階選項。 首先，而 hello 工具包含預設大量匯入的預存程序 (BulkInsert.js)，您可以選擇 toospecify 匯入預存程序：

 ![Azure Cosmos DB 大量插入 sproc 選項的螢幕擷取畫面](./media/import-data/bulkinsertsp.png)

此外，匯入日期類型時 (例如從 SQL Server 或 MongoDB)，有三種匯入選項可供選擇：

 ![Azure Cosmos DB 日期時間匯入選項的螢幕擷取畫面](./media/import-data/datetimeoptions.png)

* 字串：保存為字串值
* Epoch：保存為 Epoch 數值
* 兩者：保存字串和 Epoch 數值。 這個選項會建立子文件，例如："date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

hello Azure Cosmos DB 大量匯入工具具有 hello 下列其他進階選項：

1. 批次大小： hello 工具的預設值 tooa 批次大小為 50。  如果匯入的 hello 文件 toobe 很大，請考慮降低 hello 批次大小。 相反地，如果匯入的 hello 文件 toobe 很小，請考慮引發 hello 批次大小。
2. 指令碼大小上限 （位元組）： hello 工具預設值為 512 KB 的 tooa 最大指令碼大小
3. 停用自動 Id 產生： 如果匯入每個文件 toobe 包含識別碼欄位，然後選取此選項可提升效能。 遺漏唯一識別碼欄位的文件將不會被匯入。
4. 更新現有文件： hello 工具的預設值 toonot 取代現有的文件識別碼相衝突。 如果選取此選項，將會允許在識別碼相符時覆寫現有的文件。 對於會更新現有文件的已排定資料移轉來說，這項功能相當有用。
5. 失敗的重試次數： 指定 tooretry hello 連接 tooAzure Cosmos DB 在暫時性失敗 （例如網路連線中斷） 的 hello 次數。
6. 重試間隔： 指定多久 toowait 之間發生暫時性失敗 （例如網路連線中斷） 的 hello 連接 tooAzure Cosmos DB 重試一次。
7. 連接模式： 指定 hello 連線模式 toouse 搭配 Azure Cosmos DB。 hello 可用的選項是 DirectTcp、 DirectHttps 和閘道。 hello 直接連線模式速度較快，而 hello 閘道模式是多個防火牆易記，因為它只會使用連接埠 443。

![Azure Cosmos DB 大量匯入進階選項的螢幕擷取畫面](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> hello 匯入工具的預設值 tooconnection 模式 DirectTcp。 如果您遇到防火牆問題，請切換 tooconnection 模式閘道，因為它只需要連接埠 443。
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API （循序記錄匯入）
hello Azure Cosmos DB 循序記錄匯入工具，可讓您從任何記錄為基礎的 hello 可用的來源選項 tooimport。 如果您要匯入 tooan 已達到其配額的預存程序的現有集合，您可能會選擇此選項。 hello 工具支援匯入 tooa 單一 Azure Cosmos DB 集合 （單一資料分割和多個資料分割），以及在多個單一資料分割和/或多個資料分割的 Azure Cosmos DB 集合分割資料分割的分區化匯入。 如需分割資料的詳細資訊，請參閱 [Azure Cosmos DB 的資料分割與調整規模](partition-data.md)。

![Azure Cosmos DB 循序記錄匯入選項的螢幕擷取畫面](./media/import-data/documentdbsequential.png)

hello 的 hello Azure Cosmos DB 的連接字串的格式如下：

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

hello Azure Cosmos DB 帳戶連接字串可從擷取的 hello 金鑰刀鋒視窗中的 hello Azure 入口網站中所述[如何 toomanage Azure Cosmos DB 帳戶](manage-account.md)，不過 hello hello 資料庫名稱必須附加 toobe toohellohello 遵循格式中的連接字串：

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> 使用 hello 確認命令 tooensure hello Azure Cosmos DB hello 連接字串 欄位中指定的執行個體，可以存取。
> 
> 

tooimport tooa 單一集合中，輸入 hello 名稱 hello 集合 toowhich 資料將匯入和按一下 hello [新增] 按鈕。 tooimport toomultiple 集合、 個別輸入每個集合的名稱或使用下列語法 toospecify hello 多個集合： *collection_prefix*[start 索引-結束索引]。 當指定多個集合，透過 hello 上述語法，請記住 hello 下列：

1. 僅支援整數範圍的名稱模式。 比方說，指定集合 [0-3] 將會產生下列集合的 hello: collection0，collection1，collection2，collection3。
2. 您可以使用縮寫的語法：collection[3] 將發出一組與步驟 1 中所述相同的集合。
3. 您可以提供一個以上的替代項目。 例如，collection[0-1] [0-9] 將產生 20 個開頭為零的集合名稱 (collection01、..02、..03)。

一旦 hello 集合名稱已指定，則選擇 hello 的 hello 清查 (400 Ru too250，000 RUs) 所需的輸送量。 為了達到最佳的匯入效能，請選擇較高的輸送量。 如需效能層級的詳細資訊，請參閱 [Azure Cosmos DB 中的效能層級](performance-levels.md)。 任何匯入與輸送量 toocollections > 10,000 RUs 需要資料分割索引鍵。 如果您選擇 toohave 以上 250,000 RUs，您將需要 toofile hello 入口 toohave 增加您的帳戶的要求。

> [!NOTE]
> hello 輸送量設定僅適用於 toocollection 建立。 如果 hello 指定集合已經存在，將不會修改其輸送量。
> 
> 

當匯入 toomultiple 集合，hello 匯入工具會支援基礎的雜湊分區化。 在此案例中，指定您想 toouse hello 資料分割索引鍵為 hello 文件屬性 （如果空白的資料分割索引鍵，文件將分區化隨機跨 hello 目標集合）。

您可以選擇性地指定 hello 匯入來源中的哪一個欄位應該做為 hello Azure Cosmos DB 文件的 id 屬性期間 hello 匯入 （請注意，如果文件未包含此屬性，則 hello 匯入工具會產生 hello id 屬性值為 GUID）。

匯入期間有數個可用的進階選項。 首先，匯入日期類型時 (例如從 SQL Server 或 MongoDB)，有三種匯入選項可供選擇：

 ![Azure Cosmos DB 日期時間匯入選項的螢幕擷取畫面](./media/import-data/datetimeoptions.png)

* 字串：保存為字串值
* Epoch：保存為 Epoch 數值
* 兩者：保存字串和 Epoch 數值。 這個選項會建立子文件，例如："date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

hello Azure Cosmos DB 循序記錄匯入工具具有 hello 下列其他進階選項：

1. 平行要求的數目： hello 工具預設 too2 平行要求。 如果匯入的 hello 文件 toobe 很小，請考慮引發 hello 平行要求的數目。 請注意，如果這個數字太多，就會引發 hello 匯入可能會發生節流。
2. 停用自動 Id 產生： 如果匯入每個文件 toobe 包含識別碼欄位，然後選取此選項可提升效能。 遺漏唯一識別碼欄位的文件將不會被匯入。
3. 更新現有文件： hello 工具的預設值 toonot 取代現有的文件識別碼相衝突。 如果選取此選項，將會允許在識別碼相符時覆寫現有的文件。 對於會更新現有文件的已排定資料移轉來說，這項功能相當有用。
4. 失敗的重試次數： 指定 tooretry hello 連接 tooAzure Cosmos DB 在暫時性失敗 （例如網路連線中斷） 的 hello 次數。
5. 重試間隔： 指定多久 toowait 之間發生暫時性失敗 （例如網路連線中斷） 的 hello 連接 tooAzure Cosmos DB 重試一次。
6. 連接模式： 指定 hello 連線模式 toouse 搭配 Azure Cosmos DB。 hello 可用的選項是 DirectTcp、 DirectHttps 和閘道。 hello 直接連線模式速度較快，而 hello 閘道模式是多個防火牆易記，因為它只會使用連接埠 443。

![Azure Cosmos DB 循序記錄匯入進階選項的螢幕擷取畫面](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> hello 匯入工具的預設值 tooconnection 模式 DirectTcp。 如果您遇到防火牆問題，請切換 tooconnection 模式閘道，因為它只需要連接埠 443。
> 
> 

## <a id="IndexingPolicy"></a>建立 Azure Cosmos DB 集合時指定編製索引原則
當您允許 hello 移轉工具 toocreate 集合匯入期間時，您可以指定 hello 的 hello 集合的編製索引原則。 在 [進階選項 > 一節的 hello Azure Cosmos DB 大量匯入和 Azure Cosmos DB 循序記錄選項的 hello，瀏覽 toohello 編製索引原則] 區段中。

![Azure Cosmos DB 編製索引原則進階選項的螢幕擷取畫面](./media/import-data/indexingpolicy1.png)

使用 hello 編製索引原則的進階選項，您可以選取索引的原則檔，以手動方式輸入編製索引的原則，或選取從一組預設範本 （以滑鼠右鍵按一下中編製索引原則文字方塊中的 hello）。

hello hello 工具提供的原則範本是：

* 預設值。 當您使用 ORDER BY、範圍和數字的相等查詢針對字串進行相等查詢時，這是最佳的原則。 這個原則的索引儲存空間負擔比範圍低。
* 範圍。 當您使用 ORDER BY、範圍以及數字和字串的相等查詢時，這是最佳的原則。 這個原則的索引儲存空間負擔比預設或雜湊高。

![Azure Cosmos DB 編製索引原則進階選項的螢幕擷取畫面](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> 如果您未指定編製索引的原則，將會套用 hello 預設原則。 如需編製索引原則的詳細資訊，請參閱 [Azure Cosmos DB 編製索引原則](indexing-policies.md)。
> 
> 

## <a name="export-toojson-file"></a>匯出 tooJSON 檔案
hello Azure Cosmos DB JSON 匯出工具可讓您 tooexport 任何 hello 可用的來源選項 tooa JSON 檔案，其中包含 JSON 文件的陣列。 hello 工具將會處理 hello 匯出，或您可以選擇 tooview hello 產生移轉命令，然後自行執行 hello 命令。 在本機或 Azure Blob 儲存體中，可能會儲存 hello 產生的 JSON 檔案。

![Azure Cosmos DB JSON 本機檔案匯出選項的螢幕擷取畫面](./media/import-data/jsontarget.png)

![Azure Cosmos DB JSON Azure Blob 儲存體匯出選項的螢幕擷取畫面](./media/import-data/jsontarget2.png)

您可以選擇性地選擇 tooprettify hello 產生 JSON，會增加 hello hello 產生的文件大小，而使 hello 內容更多的人們可讀取。

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

## <a name="advanced-configuration"></a>進階組態
在 hello 進階的組態畫面中，指定您想要寫入的任何錯誤 hello 記錄檔案 toowhich hello 位置。 hello 下列規則適用於 toothis 頁面：

1. 如果未提供檔案名稱，所有的錯誤將傳回 hello [結果] 頁面。
2. 如果沒有目錄提供檔案名稱，然後 hello 檔案會建立 （或覆寫） hello 目前環境的目錄中。
3. 如果您選取的現有檔案，然後 hello 檔案將會覆寫，沒有附加選項。

然後，選擇是否 toolog 所有中的重大，或沒有錯誤訊息。 最後，決定螢幕傳輸訊息上的 hello 與它進行的更新頻率。

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>確認匯入設定及檢視命令列
1. 指定來源資訊、 目標資訊以及進階的組態之後, 檢閱 hello 移轉摘要並，選擇性地檢視/複製 hello 產生 （複製 hello 命令是有用的 tooautomate 匯入作業） 的移轉命令：
   
    ![摘要畫面的螢幕擷取畫面](./media/import-data/summary.png)
   
    ![摘要畫面的螢幕擷取畫面](./media/import-data/summarycommand.png)
2. 在您滿意來源和目標選項之後，請按一下 [匯入] 。 hello 已耗用時間、 傳送的計數，以及 （如果您並未提供 hello 進階組態中的檔案名稱） 的失敗資訊會隨著 hello 匯入正在進行更新。 完成後，您可以匯出 hello 結果 (例如 toodeal 解決任何匯入失敗)。
   
    ![Azure Cosmos DB JSON 匯出選項的螢幕擷取畫面](./media/import-data/viewresults.png)
3. 保留 hello 現有的設定 （例如連接字串資訊、 來源和目標選擇等） 或重設所有的值，您也可能會啟動新的匯入。
   
    ![Azure Cosmos DB JSON 匯出選項的螢幕擷取畫面](./media/import-data/newimport.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 安裝 hello 資料移轉工具
> * 已從不同的資料來源匯入資料
> * 從 Azure Cosmos DB tooJSON 匯出

您現在可以繼續 toohello 下一個教學課程，並了解如何使用 Azure Cosmos DB tooquery 資料。 

> [!div class="nextstepaction"]
>[如何 tooquery 資料嗎？](../cosmos-db/tutorial-query-documentdb.md)
