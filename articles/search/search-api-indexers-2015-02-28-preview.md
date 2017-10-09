---
title: "索引子作業 (Azure 搜尋服務 REST API：2015-02-28-Preview) | Microsoft Docs"
description: "索引子作業 (Azure 搜尋服務 REST API：2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>索引子作業 (Azure 搜尋服務 REST API：2015-02-28-Preview)
> [!NOTE]
> 本文說明 hello 中的索引子[2015年-02-28-preview REST API](search-api-2015-02-28-preview.md)。 此 API 版本使用文件擷取功能新增 Azure Blob 儲存體索引子和 Azure 表格儲存體索引子預覽版，加上其他改進功能。 hello API 也支援上市 (GA) 索引子，Azure SQL Database、 Azure Vm 和 Azure Cosmos DB 上的 SQL Server 包含索引子。
> 
> 

## <a name="overview"></a>概觀
Azure 搜尋可以直接整合某些常見的資料來源，移除 hello 需要 toowrite 程式碼 tooindex 您的資料。 這個向上向上 tooset，您可以呼叫 hello Azure 搜尋 API toocreate 和管理**索引子**和**資料來源**。 

**索引子** 是一種用來連接資料來源與目標搜尋索引的資源。 索引子用於 hello 下列方法： 

* 執行 hello 資料 toopopulate 索引的一次性複本。
* 同步處理索引與 hello 排程的資料來源中的變更。 hello 排程是 hello 索引子定義的一部分。
* 叫用隨 tooupdate 視需要的索引。 

**索引子**想定期更新 tooan 索引時非常有用。 您可在索引子定義中設定內嵌排程，或視需要使用 [執行索引子](#RunIndexer)加以執行。 

A**資料來源**指定哪些資料需要 toobe 編製索引，認證 tooaccess hello 資料，以及原則 tooenable Azure 搜尋 tooefficiently 識別 hello 資料 （例如修改或刪除的資料庫資料表中的資料列） 中的變更。 資料來源會被定義為獨立的資源，因此可供多個索引子使用。

目前支援下列資料來源的 hello:

* **Azure SQL Database** 和 **Azure VM 上的 SQL Server**。 如需目標逐步解說，請參閱 [本文](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)。 
* **Azure Cosmos DB**。 如需目標逐步解說，請參閱 [本文](search-howto-index-documentdb.md)。 
* **Azure Blob 儲存體**，包括 hello 下列文件格式： PDF、 Microsoft Office （DOCX/文件、 XSLX/XLS、 PPTX/PPT、 訊息）、 HTML、 XML、 ZIP 和純文字檔案 （包括 JSON）。 如需目標逐步解說，請參閱[本文](search-howto-indexing-azure-blob-storage.md)。
* **Azure 資料表儲存體**。 如需目標逐步解說，請參閱 [本文](search-howto-indexing-azure-tables.md)。

我們正在考慮未來 hello 中新增額外的資料來源的支援。 toohelp 我們排定這些決策中，請提供您的意見反應 hello [Azure 搜尋意見反應論壇](http://feedback.azure.com/forums/263029-azure-search)。

請參閱[服務限制](search-limits-quotas-capacity.md)的最大限制相關的 tooindexer 和資料來源的資源。

## <a name="typical-usage-flow"></a>一般使用流程
您可針對特定的 `data source` 或 `indexer`，使用簡單的 HTTP 要求 (POST、GET、PUT、DELETE) 以建立與管理索引子和資料來源。

一般來說，設定自動編製索引的程序有下列四個步驟：

1. 識別包含需要編製索引的 toobe hello 資料的 hello 資料來源。 請記住 Azure 搜尋可能不支援所有 hello 存在於資料來源的資料類型。 請參閱[支援的資料類型](https://msdn.microsoft.com/library/azure/dn798938.aspx)hello 清單。
2. 建立結構描述與您的資料來源相容的 Azure 搜尋服務索引。
3. 如 [建立資料來源](#CreateDataSource)所述，建立 Azure 搜尋服務的資料來源。
4. 根據 [建立索引子](#CreateIndexer)所述，建立 Azure 搜尋服務的索引子。

您應該規劃為每個目標索引和資料來源組合建立一個索引子。 您可以有多個索引子寫入至 hello 相同的索引，而且您可以重複使用 hello 相同的資料來源的多個索引子。 不過，索引子可以只使用一次一個資料來源，而且只能寫入 tooa 單一索引。 

在建立索引子之後, 您可以擷取使用 hello 的執行狀態[取得索引子狀態](#GetIndexerStatus)作業。 您也可以隨時執行索引子 (而不是，或在加法 toorunning 它排程定期上) 使用 hello[執行索引子](#RunIndexer)作業。

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>建立資料來源
在 Azure 搜尋索引子，提供臨機操作或已排程資料重新整理的目標索引的 hello 連接資訊用於資料來源。 您可以使用 HTTP POST 要求，在 Azure 搜尋服務中建立新的資料來源。

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

或者，您可以使用 PUT，並在 hello URI 上指定 hello 資料來源名稱。 如果 hello 資料來源不存在，則會建立。

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> hello 允許的資料來源數目上限因定價層。 hello 免費服務允許 too3 資料來源。 標準服務允許 50 個資料來源。 如需詳細資訊，請參閱 [服務限制](search-limits-quotas-capacity.md) 。
> 
> 

**要求**

所有服務要求都需使用 HTTPS。 hello**建立資料來源**要求可以使用 POST 或 PUT 方法建構。 使用 POST 時，您必須提供 hello 以及 hello 資料來源定義的要求主體中的資料來源名稱。 使用 PUT，hello 名稱會是 hello URL 的一部分。 如果 hello 資料來源不存在，它會建立它。 如果已經存在，則更新的 toohello 新定義。 

hello 資料來源名稱必須是小寫、 以字母或數字開頭、 不含斜線或點，和不超過 128 個字元。 啟動之後 hello 資料來源名稱以字母或數字，hello 其餘部分 hello 名稱可以包含任何字母、 數字和連字號，只要 hello 連字號不連續。 如需詳細資料，請參閱 [命名規則](https://msdn.microsoft.com/library/azure/dn857353.aspx) 。

hello`api-version`需要。 hello 新版`2015-02-28`。

**要求標頭**

hello 下列清單描述所需的 hello 和選擇性要求標頭。 

* `Content-Type`：必要。 設定得`application/json`
* `api-key`：必要。 hello`api-key`是使用的 tooauthenticate hello 要求 tooyour 搜尋服務。 它是字串值、 唯一 tooyour 服務。 hello**建立資料來源**要求必須包含`api-key`標頭設定 tooyour 管理金鑰 （為相對於的 tooa 查詢索引鍵）。 

您也需要 hello 服務名稱 tooconstruct hello 要求 URL。 您可以取得這兩個 hello 服務名稱和`api-key`從服務儀表板中 hello [Azure 入口網站](https://portal.azure.com/)。 請參閱[hello 入口網站中建立搜尋服務](search-create-service-portal.md)取得頁面導覽說明。

<a name="CreateDataSourceRequestSyntax"></a>
**要求本文語法**

hello hello 要求主體包含資料來源定義，其中包含類型的 hello 資料來源、 認證 tooread hello 資料，以及選擇性資料變更偵測和資料刪除偵測原則所使用的 tooefficiently 識別已變更或刪除時搭配定期排程的索引子的 hello 的資料來源中的資料。 

hello 建構 hello 要求裝載的語法如下所示。 本主題稍後會提供範例要求。

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

要求包含下列屬性的 hello: 

* `name`：必要。 hello hello 資料來源名稱。 資料來源名稱必須只能包含小寫字母、 數字或連字號、 無法以開頭或結尾虛線和有限的 too128 個字元。
* `description`：選用說明。 
* `type`：必要。 必須是其中一個支援的 hello 資料來源類型：
  * `azuresql` - Azure SQL Database 或 Azure VM 中的 SQL Server
  * `documentdb` - Azure Cosmos DB
  * `azureblob` - Azure Blob 儲存體
  * `azuretable` - Azure 資料表儲存體
* `credentials`：
  * 所需的 hello`connectionString`屬性會指定 hello hello 資料來源的連接字串。 hello hello 連接字串的格式取決於 hello 資料來源類型： 
    * 適用於 Azure SQL 中，這是 hello 一般 SQL Server 連接字串。 如果您使用 hello Azure 入口網站 tooretrieve hello 連接字串，使用 hello`ADO.NET connection string`選項。
    * Azure Cosmos DB hello 連接字串必須遵循格式的 hello: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`。 所有 hello 值都是必要的。 您可以在 hello [Azure 入口網站](https://portal.azure.com/)。  
    * 針對 Azure Blob 和資料表儲存體，這是 hello 儲存體帳戶連接字串。 hello 格式會描述[這裡](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/)。 需要有 HTTPS 端點通訊協定。  
* `container`需要： 指定使用 hello hello 資料 tooindex`name`和`query`屬性： 
  * `name` (必要)：
    * Azure SQL： 指定 hello 資料表或檢視表。 您可以使用符合結構描述的名稱，例如 `[dbo].[mytable]`。
    * DocumentDB： 指定 hello 集合。 
    * Azure Blob 儲存體： 指定 hello 儲存體容器。
    * Azure 資料表儲存體： 指定 hello hello 資料表名稱。 
  * `query`(選用)：
    * DocumentDB： 可讓您 toospecify 簡 Azure 搜尋可以編製索引的一般結構描述的任意 JSON 文件版面配置的查詢。  
    * Azure Blob 儲存體： 可讓您 toospecify hello blob 容器內的虛擬資料夾。 例如，針對 blob 路徑`mycontainer/documents/blob.pdf`，`documents`可用來當作 hello 虛擬資料夾。
    * Azure 資料表儲存體： 可讓您 toospecify 篩選 hello 組的資料列 toobe 匯入查詢。
    * Azure SQL：不支援查詢。 如果您需要此功能，請投票給 [這項建議](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* 選擇性的 hello`dataChangeDetectionPolicy`和`dataDeletionDetectionPolicy`屬性如下所述。

<a name="DataChangeDetectionPolicies"></a>
**資料變更偵測原則**

hello 用途的資料變更偵測原則 tooefficiently 找出已變更的資料項目。 支援的原則會根據 hello 資料來源類型而有所不同。 下節會對每項原則進行說明。 

***高水位線變更偵測原則*** 

當您的資料來源包含的資料行或符合下列準則的 hello 的屬性時，請使用此原則：

* 所有插入都會都指定 hello 資料行的值。 
* 所有更新 tooan 項目也會都變更 hello hello 資料行值。 
* hello 這個資料行值會隨著每項變更。
* 使用篩選子句類似 toohello 下列查詢`WHERE [High Water Mark Column] > [Current High Water Mark Value]`可以有效率地執行。

例如，當使用 Azure SQL 資料來源，索引的`rowversion`資料行是 hello 搭配 hello 上限標準原則使用的理想候選項目。 

您可按照下列方式來指定這項原則：

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

使用 Azure Cosmos DB 資料來源時，您必須使用 hello `_ts` Azure Cosmos DB 所提供的屬性。 

使用 Azure Blob 資料來源時，Azure 搜尋會自動使用高水位線變更偵測原則根據 blob 的上次修改時間戳記。您不需要這類原則 toospecify 自己。   

***SQL 整合式變更偵測原則***

如果您的 SQL 資料庫支援 [變更追蹤](https://msdn.microsoft.com/library/bb933875.aspx)，則建議您使用 SQL 整合式變更追蹤原則。 這項原則可讓 hello 的最高效率變更追蹤，並允許 Azure 搜尋 tooidentify 刪除資料列，而不必 toohave 您結構描述中明確的 「 虛刪除 」 資料行。

開頭為下列 SQL Server 資料庫版本的 hello 支援整合式的變更追蹤： 

* SQL Server 2008 R2 (若您使用 Azure VM 上的 SQL Server)。
* Azure SQL Database  V12 (若您使用 Azure SQL Database )。  

使用 SQL 整合式變更追蹤原則時，請不要指定個別的資料刪除偵測原則，因為本原則已內建支援刪除資料列的識別。 

這項原則僅可用於資料表，無法用於檢視表。 您需要 tooenable 變更追蹤之前，您可以使用此原則，您所使用的 hello 資料表。 如需指示，請參閱 [啟用和停用變更追蹤](https://msdn.microsoft.com/library/bb964713.aspx) 。    

建構 hello 時**建立資料來源**要求時，SQL 整合的變更追蹤原則可以指定，如下所示：

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**資料刪除偵測原則**

資料刪除偵測原則 hello 用途是 tooefficiently 識別已刪除之資料的項目。 目前，只有支援 hello 原則是 hello`Soft Delete`原則，可讓識別已刪除的項目根據 hello 值`soft delete`資料行或 hello 資料來源中的屬性。 您可按照下列方式來指定這項原則：

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> 僅支援具有字串、整數或布林值的資料行。 hello 值做為`softDeleteMarkerValue`必須是字串，即使 hello 對應資料行保有整數或布林值。 例如，如果出現在您的資料來源中的 hello 值為 1，使用`"1"`為 hello `softDeleteMarkerValue`。    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**要求本文範例**

如果您想 toouse hello 資料來源具有依排程執行索引子，此範例示範如何 toospecify 變更和刪除偵測原則： 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

如果您只想 hello 資料的一次性複製 toouse hello 資料來源，可以省略 hello 原則：

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**回應**

要求成功：「201 已建立」。 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>更新資料來源
您可以使用 HTTP PUT 要求來更新現有的資料來源。 您可以指定 hello 資料來源 tooupdate hello 名稱 hello 要求 URI:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

hello`api-version`需要。 hello 新版`2015-02-28`。 [Azure 搜尋服務 API 版本](https://msdn.microsoft.com/library/azure/dn864560.aspx)提供替代版本的詳細資訊。

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**要求**

hello 要求主體語法是 hello 一樣[建立資料來源要求](#CreateDataSourceRequestSyntax)。

無法更新現有資料來源上的某些屬性。 例如，您無法變更現有資料來源的 hello 類型。  

如果您不想要顯示現有的資料來源 toochange hello 連接字串，您可以指定常值的 hello `<unchanged>` hello 連接字串。 這是很有幫助您需要的資料來源 tooupdate 但沒有方便您存取 toohello 連接字串，因為它是機密的資料。

**回應**

對於成功的要求：如果已建立新的資料來源，會顯示「201 已建立」；如果已更新現有的資料來源，則會顯示「204 沒有內容」。

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>列出資料來源
hello**列出資料來源**作業會傳回一份 hello 資料來源中您的 Azure 搜尋服務。 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

hello`api-version`需要。 hello 新版`2015-02-28`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

要求成功：「200 確定」。

下列為回應本文的範例：

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

請注意，您可以篩選您感興趣的 toojust hello 屬性下的 hello 回應。 例如，如果您想要的資料來源名稱清單，使用 hello OData`$select`查詢選項：

    GET /datasources?api-version=205-02-28&$select=name

在此情況下，hello 回應 hello 上述範例中會出現，如下所示： 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

如果您的搜尋服務中有大量的資料來源，這是很有用的技巧 toosave 頻寬。

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>取得資料來源
hello**取得資料來源**作業會從 Azure 搜尋取得 hello 資料來源定義。

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

hello`api-version`需要。 hello 新版`2015-02-28`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

回應成功時會傳回狀態碼：200 OK。

hello 回應是中的類似 tooexamples[建立資料來源的範例要求](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> 未設定 hello`Accept`要求標頭太`application/json;odata.metadata=none`時呼叫此 API，因為這樣會導致`@odata.type`屬性 toobe 省略來自回應 hello 和您不是資料變更與資料行名稱之間能 toodifferentiate不同類型的原則。 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>刪除資料來源
hello**刪除資料來源**作業會從您的 Azure 搜尋服務中移除資料來源。

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> 如果任何索引子參考您要刪除的 hello 資料來源，hello 刪除作業仍會繼續執行。 但是，這些索引子在下一次執行時將轉換為錯誤狀態。  
> 
> 

hello`api-version`需要。 hello 新版`2015-02-28`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

狀態碼：回應成功時會傳回「204 沒有內容」。

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>建立索引子
您可以使用簡單的 HTTP POST 要求，在 Azure 搜尋服務中建立新的索引子。

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

或者，您可以使用 PUT，並在 hello URI 上指定 hello 資料來源名稱。 如果 hello 資料來源不存在，則會建立。

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> hello 允許的索引子數目上限因定價層。 hello 免費服務允許向上 too3 索引子。 標準服務允許 50 個索引子。 如需詳細資訊，請參閱 [服務限制](search-limits-quotas-capacity.md) 。
> 
> 

hello`api-version`需要。 hello 新版`2015-02-28`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

<a name="CreateIndexerRequestSyntax"></a>
**要求本文語法**

hello hello 要求主體包含索引子定義，其中指定 hello 資料來源和 hello 目標索引編製索引，以及選擇性的索引排程和參數。 

hello 建構 hello 要求裝載的語法如下所示。 本主題稍後會提供範例要求。

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**索引子排程**

索引子可以選擇性地指定排程。 如果排程存在，hello 索引子會依據排程定期執行。 排程具有下列屬性的 hello:

* `interval`：必要。 可用以指定索引子執行間隔或期間的持續時間值。 hello 最小允許值是 5 分鐘。hello 最長為一天。 其必須格式化為 XSD "dayTimeDuration" 值 ( [ISO 8601 持續時間](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) 值的受限子集)。 這個 hello 模式是： `"P[nD][T[nH][nM]]"`。 範例：`PT15M` 代表每隔 15 分鐘，`PT2H` 代表每隔 2 個小時。 
* `startTime`：必要。 UTC 日期時間 hello 索引子應該開始執行。 

**索引子參數**

您可選擇性地為索引子指定數個參數來影響其行為。 所有 hello 參數是選擇性的。  

* `maxFailedItems`： 索引子執行視為失敗之前，建立索引 hello 數可能會失敗 toobe 的項目。 預設值為 0。 失敗的項目有關的資訊由 hello[取得索引子狀態](#GetIndexerStatus)作業。 
* `maxFailedItemsPerBatch`: hello 項目數可能會失敗 toobe 索引中每個批次索引子執行視為失敗之前。 預設值為 0。
* `base64EncodeKeys`：指定文件金鑰是否要進行 base-64 編碼。 針對文件金鑰中可使用的字元，Azure 搜尋服務有加諸限制。 不過，資料來源中的 hello 值可能包含無效的字元。 如果是這類值，則文件索引鍵為必要 tooindex，此旗標可以設定 tootrue。 預設值為 `false`。
* `batchSize`： 指定以單一批次順序 tooimprove 效能的 hello hello 資料來源讀取，並且可編製索引的項目數。 hello 預設值取決於 hello 資料來源類型： 它是 SQL Azure 和 Azure Cosmos DB，1000年和 Azure Blob 儲存體的 10。

**欄位對應**

您可以使用欄位名稱的欄位對應 toomap hello 中資料來源 tooa 不同的欄位名稱 hello 目標索引中。 例如，假設來源資料表包含 `_id`欄位。 Azure 搜尋不允許欄位名稱開頭為底線，因此必須重新命名 hello 欄位。 這可以使用 hello `fieldMappings` hello 索引子，如下所示的屬性： 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

您可以指定多個欄位對應： 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

來源和目標欄位名稱皆有區分大小寫。

<a name="FieldMappingFunctions"></a>
***欄位對應函式***

欄位對應也可以使用的 tootransform 來源欄位值使用*將函數對應*。

這類函數目前僅支援一種： `jsonArrayToStringCollection`。 它會剖析包含字串 hello 目標索引 collection （edm.string） 欄位格式化為 JSON 陣列的欄位。 該函數主要用來搭配 Azure SQL 索引子，因為 SQL 不具備原生的集合資料類型。 其用法如下： 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

例如，如果 hello 來源欄位包含字串 hello `["red", "white", "blue"]`，則 hello 目標欄位的型別`Collection(Edm.String)`會填入 hello 三值`"red"`，`"white"`和`"blue"`。

請注意該 hello`targetFieldName`屬性是選擇性的; 如果省略了，hello`sourceFieldName`會使用值。 

<a name="CreateIndexerRequestExamples"></a>
**要求本文範例**

hello 下列範例會建立索引子將資料從 hello 所參考的 hello 資料表複製`ordersds`資料來源 toohello`orders`於 2015 年 1 月 1 日 UTC 會啟動並執行每小時的排程上的索引。 如果不能超過 5 個項目無法 toobe 編製索引中每個批次，而且最多 10 個項目失敗 toobe 總數，每個索引子引動過程將會成功。 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**回應**

「201 已建立」表示要求成功。

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>更新索引子
您可以使用 HTTP PUT 要求來更新現有的索引子。 您可以指定 hello 索引子 tooupdate hello 名稱 hello 要求 URI:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

hello`api-version`需要。 hello 新版`2015-02-28`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**要求**

hello 要求主體語法是 hello 一樣[建立索引子要求](#CreateIndexerRequestSyntax)。

**回應**

要求成功：如果已建立新的索引子，會顯示「201 已建立」；如果現有索引子已更新，則會顯示「204 沒有內容」。

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>列出索引子
hello**列出索引子**作業會傳回索引子的 hello 清單中您的 Azure 搜尋服務。 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


hello`api-version`需要。 hello 預覽版本`2015-02-28-Preview`。 [Azure 搜尋服務版本設定](https://msdn.microsoft.com/library/azure/dn864560.aspx) 中有提供替代版本的詳細資訊。

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

要求成功：「200 確定」。

下列為回應本文的範例：

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

請注意，您可以篩選您感興趣的 toojust hello 屬性下的 hello 回應。 例如，如果您想要的索引子名稱清單，使用 hello OData`$select`查詢選項：

    GET /indexers?api-version=2014-10-20-Preview&$select=name

在此情況下，hello 回應 hello 上述範例中會出現，如下所示： 

    {
      "value" : [ { "name": "myindexer" } ]
    }

如果您的搜尋服務中有大量索引子，這是很有用的技巧 toosave 頻寬。

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>取得索引子
hello**取得索引子**作業會從 Azure 搜尋取得 hello 索引子定義。

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

hello`api-version`需要。 hello 預覽版本`2015-02-28-Preview`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

回應成功時會傳回狀態碼：200 OK。

hello 回應是中的類似 tooexamples[建立索引子的範例要求](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>刪除索引子
hello**刪除索引子**作業會從您的 Azure 搜尋服務中移除索引子。

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

刪除索引子時，hello 索引子執行正在進行中的在該時間將執行 toocompletion，但沒有進一步的執行會排定。 找不到嘗試 toouse 不存在的索引子會導致 HTTP 狀態碼 404。 

hello`api-version`需要。 hello 預覽版本`2015-02-28-Preview`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

狀態碼：回應成功時會傳回「204 沒有內容」。

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>執行索引子
在依排程定期新增 toorunning，索引子可以也隨需叫用透過 hello**執行索引子**作業： 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

hello`api-version`需要。 hello 預覽版本`2015-02-28-Preview`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

狀態碼：回應成功時會傳回「202 已接受」。

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>取得索引子狀態
hello**取得索引子狀態**作業會擷取 hello 目前狀態和執行記錄的索引子： 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


hello`api-version`需要。 hello 預覽版本`2015-02-28-Preview`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

狀態碼：回應成功時會傳回「200 確定」。

hello 回應主體會包含有關整體索引子健全狀況狀態、 hello 最後一個索引子引動過程，以及最近索引子引動過程的 hello 歷程記錄資訊 （如果有的話）。 

範例回應本文應如下所示： 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**索引子狀態**

索引子狀態可以是 hello 的下列值的其中一個：

* `running`表示該 hello 索引子正常執行。 請注意，某些 hello 索引子執行仍然失敗，因此它是個不錯的主意 toocheck hello`lastResult`以及屬性。 
* `error`表示該 hello 索引子發生需要人為介入無法更正的錯誤。 比方說，hello 資料來源認證可能已過期，或有大幅變更 hello 結構描述或 hello 目標索引 hello 資料來源的方式。 

**索引子執行結果**

索引子執行結果包含單一索引子執行的相關資訊。 hello 最新結果會呈現為 hello `lastResult` hello 索引子狀態的屬性。 其他近期結果，如果有的話，會傳回為 hello `executionHistory` hello 索引子狀態的屬性。 

索引子執行結果會包含下列屬性的 hello: 

* `status`: hello 執行的狀態。 如需詳細資料，請參閱下方的 [索引子執行狀態](#IndexerExecutionStatus) 。 
* `errorMessage`：執行失敗的錯誤訊息。 
* `startTime`: hello 時間-utc 時區此執行開始時。
* `endTime`： 此執行結束時的 UTC hello 時間。 如果仍在進行中的 hello 執行是未設定此值。
* `errors`：項目層級的錯誤陣列 (如果有)。 每個項目皆包含文件金鑰 (`key` 屬性) 和錯誤訊息 (`errorMessage` 屬性)。 
* `itemsProcessed`: hello 的資料來源項目 （例如，資料表資料列），在此執行期間 hello 索引子嘗試 tooindex 數目。 
* `itemsFailed`: hello 的此執行期間失敗的項目數目。  
* `initialTrackingState`： 一律`null`hello 第一個索引子執行，或如果 hello 資料變更追蹤原則未啟用 hello 的資料來源使用。 如果已啟用這類原則，在後續的執行，這個值會表示 hello 第一個 （最低） 變更追蹤此執行所處理的值。 
* `finalTrackingState`： 一律`null`hello 所使用的資料來源上的 hello 資料變更追蹤原則，如果未啟用。 否則，表示 hello 最新的 （最高） 變更追蹤已順利處理由這個執行值。 

<a name="IndexerExecutionStatus"></a>
**索引子執行狀態**

索引子執行狀態擷取 hello 單一索引子執行狀態。 它可以包含下列值的 hello:

* `success`表示 hello 索引子執行已順利完成。
* `inProgress`指出 hello 索引子執行正在進行中。 
* `transientFailure` 表示正在進行索引子的執行。 如需詳細資料，請參閱 `errorMessage` 。 hello 失敗可能或可能不需要人為介入 toofix-比方說，修正 hello 資料來源之間 hello 目標索引結構描述不相容不需要使用者動作，但不會暫存資料來源停機時間。 索引子引動將繼續按照排程進行 (若有排程的話)。 
* `persistentFailure`表示該 hello 索引子失敗並需要人為介入的方式。 排程的索引子執行會停止。 之後定址 hello 問題，使用重設索引子 API toorestart hello 排定執行次數。 
* `reset`表示已重設 hello 索引子的呼叫 tooReset 索引子 API （請參閱下文）。 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>重設索引子
hello**重設索引子**作業會重設 hello 變更追蹤與 hello 索引子相關聯的狀態。 這可讓您 tootrigger 從頭重新編製索引 （例如，如果您的資料來源結構描述已變更） 或 toochange hello 資料變更偵測原則 hello 索引子相關聯的資料來源。   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

hello`api-version`需要。 hello 預覽版本`2015-02-28-Preview`。 

hello`api-key`必須是管理金鑰 （為相對於的 tooa 查詢索引鍵）。 Toohello 驗證 區段中的，請參閱[搜尋服務 REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn 深入了解索引鍵。 [在 hello 入口網站中建立搜尋服務](search-create-service-portal.md)說明 hello 要求中使用 tooget hello 服務 URL 和索引鍵屬性的方式。

**回應**

狀態碼：回應成功時會傳回「204 沒有內容」。

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>SQL 資料類型與 Azure 搜尋服務資料類型之間的對應
<table style="font-size:12">
<tr>
<td>SQL 資料類型</td>    
<td>允許的目標索引欄位類型</td>
<td>注意事項</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean、Edm.String</td>
<td></td>
</tr>
<tr>
<td>int、smallint、tinyint</td>
<td>Edm.Int32、Edm.Int64、Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64、Edm.String</td>
<td></td>
</tr>
<tr>
<td>real、float</td>
<td>Edm.Double、Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney、money<br>decimal<br>numeric
</td>
<td>Edm.String</td>
<td>Azure 搜尋服務不支援將十進位類型轉換為 Edm.Double，因為這麼做會降低準確度。
</td>
</tr>
<tr>
<td>char、nchar、varchar、nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>請參閱[欄位對應的函式](#FieldMappingFunctions)本文件的詳細資料中 tootransform 字串資料行至 collection （edm.string）</td>
</tr>
<tr>
<td>smalldatetime、datetime、datetime2、date、datetimeoffset</td>
<td>Edm.DateTimeOffset、Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>geography</td>
<td>Edm.GeographyPoint</td>
<td>支援只附帶 SRID 4326 （這是 hello 預設值） 的 POINT 類型地理位置執行個體</td>
</tr>
<tr>
<td>rowversion</td>
<td>N/A</td>
<td>資料列版本資料行不能儲存在 hello 搜尋索引，但可用於變更追蹤</td>
</tr>
<tr>
<td>time、timespan<br>binary、varbinary、image<br>xml、geometry、CLR 類型</td>
<td>N/A</td>
<td>不支援</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>JSON 資料類型與 Azure 搜尋服務資料類型之間的對應
<table style="font-size:12">
<tr>
<td>JSON 資料類型</td>    
<td>允許的目標索引欄位類型</td>
<td>注意事項</td>
</tr>
<tr>
<td>布林</td>
<td>Edm.Boolean、Edm.String</td>
<td></td>
</tr>
<tr>
<td>整數</td>
<td>Edm.Int32、Edm.Int64、Edm.String</td>
<td></td>
</tr>
<tr>
<td>浮點數</td>
<td>Edm.Double、Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>基本類型的陣列，例如 [ "a"、"b"、"c" ]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>看起來像是日期的字串</td>
<td>Edm.DateTimeOffset、Edm.String</td>
<td></td>
</tr>
<tr>
<td>GeoJSON 點物件</td>
<td>Edm.GeographyPoint</td>
<td>GeoJSON 點是在 hello 遵循格式的 JSON 物件: {「 類型 」: 「 點 」，"coordinates": [長，lat]} </td>
</tr>
<tr>
<td>其他 JSON 物件</td>
<td>N/A</td>
<td>不支援；Azure 搜尋服務目前僅支援基本類型與字串集合</td>
</tr>
</table>
