---
title: "aaaConnecting Azure SQL Database tooAzure 搜尋使用索引子 |Microsoft 文件"
description: "了解如何 toopull 資料從 Azure SQL Database tooan Azure 搜尋索引使用索引子。"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>連接 Azure SQL Database tooAzure 搜尋使用索引子

您必須先填入資料，才能搜尋 [Azure 搜尋服務索引](search-what-is-an-index.md)。 如果 hello 資料位於 Azure SQL database， **for Azure SQL Database 的 Azure 搜尋索引子**(或**Azure SQL 索引子**簡稱) 可以自動化 hello 索引程序，這表示較少的程式碼 toowrite 以及較少基礎結構 toocare 有關。

本文件涵蓋使用 hello 機制[索引子](search-indexer-overview.md)，但也會描述功能僅適用於 Azure SQL 資料庫 （例如整合式變更追蹤）。 

在加法 tooAzure SQL 資料庫中，Azure 搜尋會提供索引子[Azure Cosmos DB](search-howto-index-documentdb.md)， [Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)，和[Azure 資料表儲存體](search-howto-indexing-azure-tables.md)。 toorequest 其他資料來源的支援，提供您的意見反應 hello [Azure 搜尋意見反應論壇](https://feedback.azure.com/forums/263029-azure-search/)。

## <a name="indexers-and-data-sources"></a>索引子和資料來源

A**資料來源**指定哪些資料 tooindex，認證資料存取和有效率地識別 hello 資料 （新增、 修改或刪除資料列） 中的變更的原則。 資料來源會被定義為獨立的資源，因此可供多個索引子使用。

**索引子**是一種用來將單一資料來源連線至目標搜尋索引的資源。 索引子用於 hello 下列方法：

* 執行 hello 資料 toopopulate 索引的一次性複本。
* 更新索引與 hello 排程的資料來源中的變更。
* 執行隨 tooupdate 視需要的索引。

單一索引子可以只使用一個資料表或檢視，但如果您想要 toopopulate 多個搜尋索引，您可以建立多個索引子。 如需概念的詳細資訊，請參閱[索引子作業：一般工作流程](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow)。

您可以使用下列方式安裝及設定 Azure SQL 索引子︰

* 匯入資料精靈，在 hello [Azure 入口網站](https://portal.azure.com)
* Azure 搜尋服務 [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet)
* Azure 搜尋服務 [REST API](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations)

在本文中，我們將使用 hello REST API toocreate**索引子**和**資料來源**。

## <a name="when-toouse-azure-sql-indexer"></a>當 toouse Azure SQL 索引子
取決於數個因素與 tooyour 資料產生關聯，hello 使用 Azure SQL 索引子可能會或可能不適合。 如果您的資料放入 hello 下列需求，您可以使用 Azure SQL 索引子。

| 準則 | 詳細資料 |
|----------|---------|
| 資料來自單一資料表或檢視 | 如果 hello 資料散佈於多個資料表，您可以建立 hello 資料的單一檢視。 不過，如果您使用的檢視，您必須能夠 toouse 整合的 SQL Server 變更偵測 toorefresh 增量變更的索引。 如需詳細資訊，請參閱下列的[擷取變更及刪除的資料列](#CaptureChangedRows)。 |
| 資料類型是可相容的 | Azure 搜尋索引中支援大部分但並非全部 hello SQL 類型。 如需清單，請參閱[對應資料類型](#TypeMapping)。 |
| 不需要即時同步處理資料 | 索引子最多可以每隔五分鐘重新編製資料表的索引。 如果您的資料變更頻率及 hello 變更需要 toobe 秒或單一分鐘內反映於 hello 索引，我們建議使用 hello [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents)或[.NET SDK](search-import-data-dotnet.md) toopush 直接更新資料列。 |
| 累加式編製索引是可行的 | 如果您有大型資料集，且必須能夠使用計劃 toorun hello 索引子排程時，Azure 搜尋 tooefficiently 會識別新、 變更或刪除資料列。 如果您會視需要 (而非排程) 編製索引，或要編製索引的資料列少於 100,000 個，則僅允許進行非累加的編製索引。 如需詳細資訊，請參閱下列的[擷取變更及刪除的資料列](#CaptureChangedRows)。 |

## <a name="create-an-azure-sql-indexer"></a>建立 Azure SQL 索引子

1. 建立 hello 資料來源：

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   您可以取得 hello 連接字串從 hello [Azure 入口網站](https://portal.azure.com); 使用 hello`ADO.NET connection string`選項。

2. 如果您還沒有，建立 hello 目標 Azure 搜尋索引。 您可以建立使用 hello 索引[入口網站](https://portal.azure.com)或 hello[建立索引 API](https://docs.microsoft.com/rest/api/searchservice/Create-Index)。 請確定該 hello 的目標索引結構描述是與 hello hello 來源資料表的結構描述相容-請參閱[SQL 與 Azure 搜尋之間對應資料類型](#TypeMapping)。

3. 建立 hello 索引子以名稱並參考 hello 資料來源和目標索引：

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

以這種方式建立索引子不需依照排程。 索引子一旦建立好就會自動執行。 您可以在任何時候使用 **執行索引子** 要求再執行一次：

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

您可以自訂數個層面的索引子行為，例如，批次處理大小，以及在索引子執行失敗前可略過多少份文件。 如需詳細資訊，請參閱[建立索引子 API](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer)。

您可能需要 tooallow Azure 服務 tooconnect tooyour 資料庫。 請參閱[從 Azure 連線](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure)如需有關指示 toodo 的。

toomonitor hello 索引子狀態和執行歷程記錄 （編製索引的項目數目、 失敗等），請使用**索引子狀態**要求：

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

hello 回應應該看起來類似 toohello 下列：

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

執行記錄包含已 too50 （以便 hello 回應 hello 最新的執行為優先） 以 hello 反向時間順序排序的 hello 最近完成執行。
Hello 回應的其他資訊位於[取得索引子狀態](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>依照排程執行索引子
您也可以排列 hello 索引子 toorun 定期排程上。 toodo，新增 hello**排程**時建立或更新 hello 索引子的屬性。 hello 下面範例是 PUT 要求 tooupdate hello 索引子：

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

hello**間隔**參數是必要項。 hello 間隔是指 toohello hello 開頭的兩個連續的索引子執行之間的時間。 hello 最小允許值是 5 分鐘。hello 最長為一天。 其必須格式化為 XSD "dayTimeDuration" 值 ( [ISO 8601 持續時間](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) 值的受限子集)。 這個 hello 模式是： `P(nD)(T(nH)(nM))`。 範例：`PT15M` 代表每隔 15 分鐘，`PT2H` 代表每隔 2 個小時。

選擇性的 hello **startTime**指出當 hello 的排定的執行數目應該開始。 如果省略，則會使用 hello 目前 UTC 時間。 此時可以是過去 – 如同 hello 索引子執行持續自 hello startTime hello 第一次執行已在此情況下排程 hello。  

索引子一次僅能執行一個。 索引子執行已排程執行時，如果 hello 執行會延後到 hello 下次排程時間。

讓我們看一下範例 toomake 這更具體。 假設我們 hello 下列設定的每小時排程：

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

排程狀況如下：

1. hello 第一次索引子執行開始在或前後 2015 年 3 月 1 日上午 12:00 UTC。
2. 假設此執行需要 20 分鐘 (或任何小於 1 小時的時間)。
3. hello 第二次執行開始在或前後 2015 年 3 月 1 日上午 1:00
4. 現在，假設此執行需要超過一小時 (例如 70 分鐘)，因此會在上午 2:10 左右完成。
5. 第三個執行 toostart hello 時間上午 2:00，現在是它。 不過，因為 hello 上午 1 第二次執行 仍在執行中，會略過 hello 第三次執行。 會在凌晨 3 hello 第三個執行

您可以使用 **PUT 索引子** 要求，加入、 變更或刪除現有之索引子的排程。

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>擷取新增、變更和刪除的資料列

Azure 搜尋會使用**累加索引**tooavoid toore 索引 hello 整份資料表或檢視每次索引子執行。 Azure 搜尋會提供兩個變更偵測原則 toosupport 累加編製索引。 

### <a name="sql-integrated-change-tracking-policy"></a>SQL 整合變更追蹤原則
如果您的 SQL 資料庫支援 [變更追蹤](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server)，則建議您使用 **SQL 整合式變更追蹤原則**。 這是 hello 最有效率的原則。 此外，它可讓 Azure 搜尋 tooidentify 刪除資料列不需要您 tooadd tooyour 明確的 「 虛刪除 」 資料行的資料表。

#### <a name="requirements"></a>需求 

+ 資料庫版本需求：
  * SQL Server 2012 SP3 和更新版本 (若您在 Azure VM 上使用 SQL Server)。
  * Azure SQL Database  V12 (若您使用 Azure SQL Database )。
+ 僅限資料表 (沒有檢視)。 
+ Hello 資料庫上[啟用變更追蹤](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server)hello 資料表。 
+ 沒有複合主索引鍵 （主索引鍵包含超過一個資料行） hello 資料表上。  

#### <a name="usage"></a>使用量

toouse 此原則，建立或更新您的資料來源，就像這樣：

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

使用 SQL 整合式變更追蹤原則時，請不要指定個別的資料刪除偵測原則，因為本原則已內建支援刪除資料列的識別。 不過，如 hello 刪除 toobe 偵測到 「 自動 」，搜尋索引中的 hello 文件索引鍵必須是 hello 與 hello hello SQL 資料表中的主索引鍵相同。 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>上限標準變更偵測原則

此變更偵測原則會依賴 「 上限標記 」 資料行擷取 hello 版本或資料列上次更新的時間。 若您使用檢視，就必須使用上限標準原則。 hello 高上限標記資料行必須符合下列需求的 hello。

#### <a name="requirements"></a>需求 

* 所有插入都會都指定 hello 資料行的值。
* 所有更新 tooan 項目也會都變更 hello hello 資料行值。
* hello 這個資料行值會隨著每個 insert 或 update。
* 查詢與 hello 遵循 WHERE 和 ORDER BY 子句可以有效率地執行：`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> 我們強烈建議使用 hello [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) hello 高上限標記資料行資料類型。 如果使用其他任何資料類型時，變更追蹤不一定的 toocapture hello 存在與索引子查詢同時執行的交易中的所有變更。 當使用**rowversion**中具有唯讀複本的組態，您必須指向 hello 索引子 hello 主要複本。 只有主要複本可用於資料同步處理案例。

#### <a name="usage"></a>使用量

toouse 上限標準原則，來建立或更新資料來源如下：

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> 如果 hello 來源資料表沒有 hello 高上限標記資料行的索引，hello SQL 索引子所使用的查詢可能會逾時。特別是，hello`ORDER BY [High Water Mark Column]`子句時，便需要索引 toorun 有效率地 hello 資料表包含多個資料列。
>
>

如果您遇到逾時錯誤，您可以使用 hello`queryTimeout`索引子的組態設定 tooset hello 查詢逾時 tooa 值高於 hello 預設 5 分鐘的逾時。 例如，tooset hello 逾時 too10 分鐘數，建立或更新 hello 索引子以 hello 下列組態：

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

您也可以停用 hello`ORDER BY [High Water Mark Column]`子句。 不過，建議您不要因為如果 hello 索引子執行已因錯誤而中斷，hello 索引子具有 toore 同處理序的所有資料列如果稍後-執行即使 hello 索引子 hello 中斷的時間已經處理 hello 的幾乎所有資料列。 toodisable hello`ORDER BY`子句中，使用 hello `disableOrderByHighWaterMarkColumn` hello 索引子定義中設定：  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>虛刪除資料行刪除偵測原則
當資料列會從 hello 來源資料表刪除時，您可能想 toodelete hello 搜尋索引的資料列。 如果您使用 hello SQL 整合變更追蹤原則，這是為您處理。 不過，hello 上限標準變更追蹤原則不會協助您刪除的資料列。 哪些 toodo？

如果 hello 資料列會實際移除 hello 資料表中，Azure 搜尋會有不存在的記錄沒有方式 tooinfer hello 存在。  不過，您可以使用 hello 「 虛刪除 」 技術 toologically 刪除資料列，而不需移除 hello 資料表。 加入資料行 tooyour 資料表或檢視表，並將資料列標示為已刪除使用該資料行。

當使用 hello 虛刪除的技術，您可以指定 hello 虛刪除原則，如下所示建立或更新 hello 資料來源時：

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

hello **softDeleteMarkerValue**必須是字串 – 使用您的實際值 hello 字串表示。 例如，如果您有整數資料行都具有 hello 值 1 標示為刪除的資料列時，使用`"1"`。 如果您以布林值 true hello 標示為刪除的資料列的位元資料行，請使用`"True"`。

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>SQL 與 Azure 搜尋服務資料類型之間的對應
| SQL 資料類型 | 允許的目標索引欄位類型 | 注意事項 |
| --- | --- | --- |
| bit |Edm.Boolean、Edm.String | |
| int、smallint、tinyint |Edm.Int32、Edm.Int64、Edm.String | |
| bigint |Edm.Int64、Edm.String | |
| real、float |Edm.Double、Edm.String | |
| smallmoney、money 十進位數值 |Edm.String |Azure 搜尋服務不支援將十進位類型轉換為 Edm.Double，因為這麼做會降低準確度。 |
| char、nchar、varchar、nvarchar |Edm.String<br/>Collection(Edm.String) |如果 hello 字串代表 JSON 陣列的字串，SQL 字串可以是使用的 toopopulate collection （edm.string） 欄位：`["red", "white", "blue"]` |
| smalldatetime、datetime、datetime2、date、datetimeoffset |Edm.DateTimeOffset、Edm.String | |
| uniqueidentifer |Edm.String | |
| geography |Edm.GeographyPoint |支援只附帶 SRID 4326 （這是 hello 預設值） 的 POINT 類型地理位置執行個體 |
| rowversion |N/A |資料列版本資料行不能儲存在 hello 搜尋索引，但可用於變更追蹤 |
| time、timespan、binary、varbinary、image、xml、geometry、CLR 類型 |N/A |不支援 |

## <a name="configuration-settings"></a>組態設定
SQL 索引子公開數個組態設定︰

| 設定 | 資料類型 | 目的 | 預設值 |
| --- | --- | --- | --- |
| queryTimeout |字串 |設定 hello SQL 查詢執行逾時 |5 分鐘 ("00:05:00") |
| disableOrderByHighWaterMarkColumn |布林 |會導致 hello hello 上限標準原則 tooomit hello ORDER BY 子句使用的 SQL 查詢。 請參閱[上限標準原則](#HighWaterMarkPolicy) |false |

這些設定會用於 hello `parameters.configuration` hello 索引子定義中的物件。 例如，tooset hello 查詢逾時 too10 分鐘數，建立或更新 hello 索引子以 hello 下列組態：

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>常見問題集

**問：我可以在 Azure 中搭配在 IaaS VM 上執行的 SQL 資料庫，使用 Azure SQL 索引子嗎？**

是。 不過，您需要 tooallow 搜尋服務 tooconnect tooyour 資料庫。 如需詳細資訊，請參閱[Azure VM 上設定從 Azure 搜尋索引子 tooSQL 伺服器連線](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md)。

**問：我可以搭配在內部部署執行的 SQL 資料庫，使用 Azure SQL 索引子嗎？**

無法直接進行。 我們不要建議或支援直接連線，因為這樣做，需要您 tooopen 資料庫 tooInternet 流量。 客戶需要使用像是 Azure Data Factory 的橋接器技術，才能成功執行此案例。 如需詳細資訊，請參閱[使用 Azure Data Factory 的推播資料 tooan Azure 搜尋索引](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector)。

**問：在 Azure 上，除了在 IaaS 中執行的 SQL Server，能夠搭配其他資料庫使用 Azure SQL 索引子嗎？**

否。 我們不支援此案例中，因為我們尚未測試 hello 和 SQL Server 以外的任何資料庫的索引子。  

**問：可以建立多個依照排程執行的索引子嗎？**

是。 但是一次只能在一個節點上執行一個索引子。 如果您需要同時執行多個索引子時，請考慮向上擴充比一個搜尋單位您搜尋服務 toomore。

**問：執行索引子會影響我的查詢工作負載嗎？**

是。 索引子執行的其中一個在您的搜尋服務中的 hello 節點，該節點的資源編製索引及查詢流量和其他應用程式開發介面要求提供服務之間共用。 如果您密集執行索引及查詢工作負載，且經常遇到 503 錯誤或回應次數增加，請考慮[調整您的搜尋服務](search-capacity-planning.md)。

**問：是否可以在[容錯移轉叢集](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)中使用次要複本作為資料來源？**

這要看狀況。 針對完整編製索引的資料表或檢視，您可以使用次要複本。 

針對累加式編製索引，Azure 搜尋服務支援兩個變更偵測原則：SQL 整合變更追蹤與上限標準。

在唯讀複本中，SQL 資料庫不支援整合變更追蹤。 因此，您必須使用上限標準原則。 

一般建議是 toouse hello rowversion hello 高上限標記資料行的資料類型。 不過，使用 rowversion 依賴 SQL Database 的 `MIN_ACTIVE_ROWVERSION` 函式，但唯讀複本上不支援此函式。 因此，您必須指向 hello 索引子 tooa 主要複本，如果您使用 rowversion。

如果您嘗試在唯讀複本 toouse rowversion 時，您會看到下列錯誤 hello: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**問：我是否可以針對上限標準變更追蹤使用替代的非 rowversion 資料行？**

我們不建議這樣做。 僅允許使用 **rowversion** 進行可靠的資料同步處理。 不過，根據您的應用程式邏輯而定，如果符合下列情況，則它可能是安全：

+ 您可以確保 hello 索引子執行時，沒有 hello 進行索引的資料表上未處理的交易 （例如，資料表的所有更新，就可能都發生以批次的排程、 和 hello Azure 搜尋索引子排程設定與 hello 資料表重疊 tooavoid更新排程）。  

+ 您定期進行完整重新索引 toopick 任何遺失的資料列。 
