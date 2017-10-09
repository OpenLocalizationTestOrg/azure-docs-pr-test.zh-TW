---
title: "Azure 搜尋的 Cosmos DB 資料來源 aaaIndexing |Microsoft 文件"
description: "本文章將示範如何 toocreate Azure 搜尋索引子以 Cosmos DB 做為資料來源。"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>使用索引子連接 Cosmos DB 與 Azure 搜尋服務

如果您想的 tooimplement 絕佳搜尋經驗您 Cosmos DB 的資料時，您可以使用 Azure 搜尋索引子 toopull 資料到 Azure 搜尋索引。 在本文中，我們會示範如何 toointegrate Azure Cosmos DB，使用 Azure 搜尋而不需要 toowrite 任何程式碼 toomaintain 索引基礎結構。

tooset Cosmos DB 索引子上的，您必須擁有[Azure 搜尋服務](search-create-service-portal.md)，並建立索引、 資料來源，和最後 hello 索引子。 您可以建立這些物件正在使用 hello[入口網站](search-import-data-portal.md)， [.NET SDK](/dotnet/api/microsoft.azure.search)，或[REST API](/rest/api/searchservice/)所有非.NET 語言。 

如果您選擇 hello 入口網站，hello[匯入資料精靈](search-import-data-portal.md)會引導您完成所有這些資源的 hello 建立。

> [!NOTE]
> Cosmos DB 為 hello DocumentDB 的下一個層代。 雖然 hello 產品名稱變更，語法是 hello 相同和以前一樣。 請繼續 toospecify`documentdb`這個索引子發行項中的指示。 

> [!TIP]
> 您可以啟動 hello**匯入資料**hello Cosmos DB 儀表板 toosimplify 編製索引的該資料來源中的精靈。 在左瀏覽到 太**集合** > **加入 Azure 搜尋**tooget 啟動。

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Azure 搜尋服務索引子概念
Azure 搜尋支援 hello 建立和管理資料來源 （包括 Cosmos DB） 和索引子，會針對這些資料來源運作。

A**資料來源**指定 hello 資料 tooindex、 認證和原則來識別 hello 資料 （例如您的集合內的已修改或刪除文件） 中的變更。 hello 資料來源定義為獨立的資源，因此可供多個索引子。

**索引子**描述 hello 資料流動的方式從資料來源到目標搜尋索引。 索引子可用來：

* 執行 hello 資料 toopopulate 索引的一次性複本。
* 同步處理索引與 hello 排程的資料來源中的變更。 hello 排程是 hello 索引子定義的一部分。
* 視需要更新 tooan 索引視需要來叫用。

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>步驟 1：建立資料來源
toocreate 資料來源，執行 POST 作業：

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

hello hello 要求主體包含 hello 資料來源定義，其中應包含下列欄位的 hello:

* **名稱**： 選擇任何名稱 toorepresent Cosmos DB 資料庫。
* **type**：必須是 `documentdb`。
* **認證**：
  
  * **connectionString**：必要。 指定下列格式的 hello hello 連線資訊 tooyour Azure Cosmos DB 資料庫：`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **容器**：
  
  * **名稱**：必要。 指定 hello 識別碼 hello Cosmos DB 集合 toobe 編製索引。
  * **查詢**：選擇性。 您可以指定查詢 tooflatten 任意 JSON 文件到 Azure 搜尋可以編製索引的一般結構描述。
* **dataChangeDetectionPolicy**：建議使用。 請參閱[索引變更的文件](#DataChangeDetectionPolicy)小節。
* **dataDeletionDetectionPolicy**：選擇性。 請參閱[索引刪除的文件](#DataDeletionDetectionPolicy)小節。

### <a name="using-queries-tooshape-indexed-data"></a>使用查詢 tooshape 編製索引的資料
您可以指定 Cosmos DB 查詢 tooflatten 巢狀屬性或陣列專案 JSON 屬性和篩選 hello 資料 toobe 編製索引。 

範例文件︰

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

篩選查詢：

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

壓平合併查詢︰

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
投影查詢：

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


陣列壓平合併查詢︰

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>步驟 2：建立索引
建立目標 Azure 搜尋服務索引 (如果您尚未建立)。 您可以建立使用 hello 索引[Azure 入口網站 UI](search-create-index-portal.md)，hello[建立索引 REST API](/rest/api/searchservice/create-index)或[Index 類別](/dotnet/api/microsoft.azure.search.models.index)。

hello 下列範例會建立索引的識別碼和描述欄位：

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

請確定該 hello 的目標索引結構描述是與 hello hello 來源 JSON 文件的結構描述或 hello 輸出的自訂查詢投影相容。

> [!NOTE]
> 對於資料分割的集合，hello 預設文件索引鍵是 Cosmos DB`_rid`屬性，重新命名過`rid`Azure 搜尋中。 此外，Cosmos DB 的 `_rid` 值包含 Azure 搜尋服務索引鍵中無效的字元。 基於這個理由，hello`_rid`值是以 Base64 編碼。
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>JSON 資料類型與 Azure 搜尋服務資料類型之間的對應
| JSON 資料類型 | 相容的目標索引欄位類型 |
| --- | --- |
| Bool |Edm.Boolean、Edm.String |
| 看起來像是整數的數字 |Edm.Int32、Edm.Int64、Edm.String |
| 看起來像是浮點的數字 |Edm.Double、Edm.String |
| String |Edm.String |
| 基本類型的陣列，例如 ["a", "b", "c"] |Collection(Edm.String) |
| 看起來像是日期的字串 |Edm.DateTimeOffset、Edm.String |
| GeoJSON 物件，例如 { "type": "Point", "coordinates": [long, lat] } |Edm.GeographyPoint |
| 其他 JSON 物件 |N/A |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>步驟 3：建立索引子

一旦已建立 hello 索引和資料來源，就要準備好 toocreate hello 索引子：

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

這個索引子執行每隔兩小時 (排程間隔設定得 「 PT2H")。 索引子 toorun 每隔 30 分鐘、 設定 hello 間隔太"PT30M"。 hello 最短支援的間隔是 5 分鐘。 hello 排程是選用-如果省略，索引子會執行一次建立時。 不過，您隨時都可依需求執行索引子。   

如需有關 hello 建立索引子 API，請簽出[建立索引子](https://docs.microsoft.com/rest/api/searchservice/create-indexer)。

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>視需要執行索引子
在依排程定期新增 toorunning，索引子可以也隨需叫用：

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> 當執行 API 傳回成功時，已排定 hello 索引子引動過程，但 hello 實際的處理會以非同步方式。 

您可以監視 hello hello 入口網站或使用 hello 取得索引子狀態 API，其接下來，我們說明中的索引子狀態。 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>取得索引子狀態
您可以擷取索引子的 hello 狀態和執行記錄：

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

hello 回應包含整體索引子狀態、 hello 最後一個 （或進行中） 的索引子引動過程和 hello 記錄的最新的索引子引動過程。

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

執行記錄包含已 toohello 50 最近完成執行，這會依反向時間順序來排序 （因此 hello 回應 hello 最新的執行為優先）。

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>索引已變更的文件
hello 用途的資料變更偵測原則 tooefficiently 找出已變更的資料項目。 目前，只有支援 hello 原則是 hello`High Water Mark`原則使用 hello `_ts` （時間戳記） 所提供屬性，由 Cosmos DB 的指定方式如下：

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

此原則強烈建議使用 tooensure 良好的索引子的效能。 

如果您使用自訂查詢，確定該 hello`_ts`屬性投射 hello 查詢。

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>累加進度與自訂查詢
建立索引期間的累加進度可確保索引子執行將會中斷暫時性失敗所執行的時間限制，如果 hello 索引子可以挑選中斷的位置下一次它執行，而不需從頭 toore 索引 hello 整個集合。 這在建立大型集合的索引時尤其重要。 

tooenable 累加進度時使用自訂查詢，確保您的查詢將依照 hello 來排序結果 hello`_ts`資料行。 這可讓定期檢查指 Azure 搜尋會使用 tooprovide 累加進度中的失敗 hello 是否存在。   

在某些情況下，即使您的查詢包含`ORDER BY [collection alias]._ts`子句，Azure 搜尋可能會推斷該 hello 查詢依 hello `_ts`。 您可以告訴 Azure 搜尋結果會依使用 hello 排序`assumeOrderByHighWaterMarkColumn`組態屬性。 toospecify 此提示，來建立或更新索引子，如下所示： 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>索引已刪除的文件
當從 hello 集合，會刪除資料列時，您通常想 toodelete hello 搜尋索引的資料列。 資料刪除偵測原則 hello 用途是 tooefficiently 識別已刪除之資料的項目。 目前，只有支援 hello 原則是 hello`Soft Delete`原則 （刪除標示為以某種類型的旗標），其中的指定方式如下：

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

如果您使用自訂查詢，確定所參考的 hello 屬性`softDeleteColumnName`hello 查詢投射。

下列範例中的 hello 虛刪除原則以建立資料來源：

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>接續步驟
恭喜！ 您已經學會如何使用 Azure 搜尋 toointegrate Azure Cosmos DB hello 索引子 Cosmos DB。

* toolearn 如何深入了解 Azure Cosmos DB，請參閱 hello [Cosmos DB 服務頁面](https://azure.microsoft.com/services/documentdb/)。
* toolearn 如何進一步了解 Azure 搜尋中，請參閱 hello[搜尋服務頁面](https://azure.microsoft.com/services/search/)。
