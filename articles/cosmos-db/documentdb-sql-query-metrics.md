---
title: "Azure Cosmos DB DocumentDB api aaaSQL 查詢度量資訊 |Microsoft 文件"
description: "深入了解 tooinstrument 和偵錯 hello Azure Cosmos 資料庫要求的 SQL 查詢效能。"
keywords: "sql 語法, sql 查詢, sql 查詢, json 查詢語言, 資料庫概念和 sql 查詢, 彙總函式"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>使用 Azure Cosmos DB 調整查詢效能
Azure Cosmos DB 提供一個[適用於查詢資料的 SQL API](documentdb-sql-query.md)，而不需結構描述或次要索引。 本文提供下列資訊適用於開發人員的 hello:

* 關於 Azure Cosmos DB 之 SQL 查詢執行如何運作的高階詳細資料
* 關於查詢要求和回應標頭以及用戶端 SDK 選項的詳細資訊
* 查詢效能的秘訣和最佳作法
* Tooutilize SQL 執行統計資料 toodebug 如何查詢效能的範例

## <a name="about-sql-query-execution"></a>關於 SQL 查詢執行

在 Azure Cosmos DB 中，您將資料儲存在 tooany 所能成長的容器[儲存體大小或要求輸送量](partition-data.md)。 Azure Cosmos DB 順暢地調整資料在 hello 涵蓋 toohandle 資料成長或佈建輸送量增加下的實體資料分割。 您可以發出 SQL 查詢 tooany 容器使用 hello REST API 或其中一個支援的 hello [DocumentDB Sdk](documentdb-sdk-dotnet.md)。

分割的簡短概觀：您定義分割區索引鍵 (例如 "city")，以決定在實體分割區之間分割資料的方式。 資料隸屬 tooa 單一資料分割索引鍵 (，例如"city"= = 「 西雅圖 」) 儲存在實體資料分割，但通常單一的實體資料分割有多個資料分割索引鍵。 當資料分割達到其儲存體大小時，hello 服務順暢地 hello 資料分割分成兩個新的資料分割，並在這些資料分割之間平均除以 hello 資料分割索引鍵。 由於資料分割是暫時性的 hello 應用程式開發介面使用 「 資料分割索引鍵範圍 」，代表 hello 範圍的資料分割索引鍵的雜湊的摘要。 

當您發出查詢 tooAzure Cosmos DB 時，hello SDK 就會執行下列邏輯步驟：

* 剖析 hello SQL 查詢 toodetermine hello 查詢執行計畫。 
* 如果 hello 查詢包含篩選與 hello 資料分割索引鍵，如`SELECT * FROM c WHERE c.city = "Seattle"`，它是路由的 tooa 單一資料分割。 如果 hello 查詢並沒有篩選的資料分割索引鍵，則執行的所有資料分割，而且結果會合併用戶端。
* hello 查詢是在數列中每個資料分割內執行，或平行，根據用戶端設定。 內每個資料分割，hello 查詢可能會讓其中一個或多個往返根據 hello 查詢複雜度，設定頁面大小和佈建輸送量 hello 集合。 每次執行會傳回 hello 數目[要求單位](request-units.md)耗用執行查詢，並選擇性地查詢執行統計資料。 
* hello SDK 會在資料分割之間執行 hello 查詢結果的摘要。 比方說，如果 hello 查詢牽涉到橫跨資料分割的 ORDER BY，然後從個別資料分割的結果是合併排序 tooreturn 結果全域依排序順序。 如果 hello 查詢之類的彙總`COUNT`，個別的資料分割中的 hello 計數會加總的 tooproduce hello 總數。

hello Sdk 提供查詢執行的各種選項。 例如，在.NET 中就使用這些選項在 hello`FeedOptions`類別。 hello 下表描述這些選項，以及它們如何影響查詢執行時間。 

| 選項 | 說明 |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | 必須設定 tootrue 需要 toobe 跨多個分割區執行任何查詢。 這是明確的旗標 tooenable 您開發期間的 toomake 做出明智的效能取捨。 |
| `EnableScanInQuery` | 必須設定 tootrue 如果您已選擇不建立索引，但仍想透過掃描 toorun hello 查詢。 只適用於索引 hello 要求已停用篩選路徑。 | 
| `MaxItemCount` | hello 的每個往返 toohello 伺服器的項目 tooreturn 數目上限。 藉由設定太-1，您可以讓 hello 伺服器管理 hello 項目數目。 或者，您可以降低此值 tooretrieve 只有少數往返每項目。 
| `MaxBufferedItemCount` | 這是用戶端的選項，而且執行跨資料分割 ORDER BY 時，使用 toolimit hello 記憶體耗用量。 較高值有助於減少 hello 延遲的排序方式跨資料分割。 |
| `MaxDegreeOfParallelism` | 取得或設定執行用戶端 hello Azure DocumentDB 資料庫服務中的平行查詢執行期間的並行作業的 hello 數目。 正值的屬性值會限制並行作業 toohello 設定值的 hello 數目。 如果它設定為大於 0 的 tooless，hello 系統會自動決定 hello toorun 並行作業數。 |
| `PopulateQueryMetrics` | 啟用在查詢執行的各種階段 (例如，編譯時間、索引迴圈時間及文件載入時間) 所花費時間的統計資料詳細記錄。 Azure 支援 toodiagnose 查詢效能問題，您可以共用從 查詢統計資料的輸出。 |
| `RequestContinuation` | 您可以藉由任何查詢所傳回的 hello 不透明的接續 token，傳遞繼續執行查詢。 hello 接續 token 封裝所需的查詢執行的所有狀態。 |
| `ResponseContinuationTokenLimitInKb` | 您可以限制 hello hello 伺服器所傳回的 hello 接續 token 的大小上限。 您可能需要 tooset 這如果應用程式主機都有回應標頭大小限制。 將此設定可能會增加 hello 整體持續期間和 RUs 所耗用的 hello 查詢。  |

比方說，我們的範例查詢要求與集合上的資料分割索引鍵上`/city`為 hello 資料分割索引鍵且佈建 100,000 RU/秒的輸送量。 您要求此查詢使用`CreateDocumentQuery<T>`.net hello 如下：

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

hello SDK 程式碼片段，如上所示對應 toohello 下列 REST API 要求：

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

每個查詢執行頁面對應 tooa REST API`POST`以 hello`Accept: application/query+json`標頭，並且在 hello 主體中的 hello SQL 查詢。 每個查詢可讓一或多個四捨五入往返 toohello 伺服器以 hello`x-ms-continuation`回應 hello tooresume 執行用戶端和伺服器之間的語彙基元。 在 FeedOptions hello 組態選項會傳遞 toohello hello 表單的要求標頭中的伺服器。 例如，`MaxItemCount`太對應`x-ms-max-item-count`。 

hello 要求會傳回 （截斷來提高可讀性） hello 下列回應：

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

hello 索引鍵的回應標頭 hello 查詢所傳回的 hello 如下：

| 選項 | 說明 |
| ------ | ----------- |
| `x-ms-item-count` | hello hello 回應中傳回的項目數目。 這是取決於提供的 hello `x-ms-max-item-count`，hello hello 回應承載大小上限、 hello 佈建的輸送量和查詢執行時間內可容納的項目數目。 |  
| `x-ms-continuation:` | hello 接續權杖 tooresume 執行 hello 查詢，如果其他結果可供使用。 | 
| `x-ms-documentdb-query-metrics` | hello hello 執行的查詢統計資料。 這是時間的分隔的字串，包含花費在 hello 各階段的查詢執行統計資料。 時所傳回`x-ms-documentdb-populatequerymetrics`設定得`True`。 | 
| `x-ms-request-charge` | hello 數目[要求單位](request-units.md)hello 查詢所取用。 | 

如需 hello REST API 的要求標頭和選項的詳細資訊，請參閱[查詢使用 hello DocumentDB REST API 資源](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api)。

## <a name="best-practices-for-query-performance"></a>查詢效能的最佳作法
hello 如下 hello 最常見因素會影響 Azure Cosmos DB 查詢效能。 我們將在本文中更深入探討下列每個主題。

| 因素 | 秘訣 | 
| ------ | -----| 
| 佈建的輸送量 | 測量 RU 每個查詢，並確認您擁有 hello 需要佈建的輸送量您的查詢。 | 
| 分割區和分割區索引鍵 | 查詢，而非 hello 資料分割索引鍵值的低延遲的 hello 篩選子句中。 |
| SDK 與查詢選項 | 遵循 SDK 最佳作法 (例如直接連線)，並調整用戶端查詢執行選項。 |
| 網路延遲 | 負責網路額外負荷中測量，並使用多路連接的應用程式開發介面 tooread hello 從最接近的區域。 |
| 索引原則 | 確定您擁有 hello 需要編製索引的路徑/原則 hello 查詢。 |
| 查詢執行計量 | 分析 hello 查詢執行度量 tooidentify 潛在撰寫查詢與資料的圖形。  |

### <a name="provisioned-throughput"></a>佈建的輸送量
在 Cosmos DB 中，您會建立資料的容器，每一個容器都具有以每秒要求單位 (RU) 表示的保留輸送量。 讀取 1 KB 文件為 1 RU 和每一項作業 （包括查詢） 是正規化的 tooa 固定數目 RUs 根據它的複雜度。 例如，如果您已針對容器佈建了 1000 RU/秒，且具有類似 `SELECT * FROM c WHERE c.city = 'Seattle'` 的查詢 (其取用 5 RU)，則您每秒可執行 (1000 RU/秒) / (5 RU/查詢) = 200 個查詢/秒之類的查詢。 

如果您提交 200 個以上的查詢/sec，超過 200/s 的速率限制連入要求會啟動 hello 服務。 hello Sdk 自動處理這種情況，藉由執行輪詢/重試，因此您可能會注意到這些查詢較高的延遲。 增加 hello 佈建輸送量 toohello 需要值可改善您的查詢延遲和輸送量。 

toolearn 有關要求單位的詳細資訊請參閱[要求單位](request-units.md)。

### <a name="partitioning-and-partition-keys"></a>分割區和分割區索引鍵
以 Azure Cosmos DB，通常是查詢中的執行順序，從最快的/最有效率 tooslower/較有效率的 hello。 

* 單一分割區索引鍵和項目索引鍵上的 GET
* 單一分割區索引鍵上具有篩選子句的查詢
* 任何屬性上不具等號比較或範圍篩選子句的查詢
* 不含篩選的查詢

查詢該需要 tooconsult 所有資料分割需要較高的延遲，並可使用更高版本的俄文。 因為每個資料分割具有自動檢索，針對所有屬性，所以 hello 查詢可以有效地從處理 hello 索引在此情況下。 您可以讓查詢更快的磁碟分割跨越透過 hello 平行處理原則的選項。

toolearn 深入了解資料分割和資料分割索引鍵，請參閱[分割在 Azure Cosmos DB](partition-data.md)。

### <a name="sdk-and-query-options"></a>SDK 與查詢選項
請參閱[效能祕訣](performance-tips.md)和[效能測試](performance-testing.md)如 tooget hello Azure Cosmos DB 從用戶端效能最佳的方式。 這包括使用 hello 最新的 Sdk，設定平台專屬組態，例如 預設的連接數目，記憶體回收的頻率，並使用輕量級的連線選項，例如直接/TCP。 


#### <a name="max-item-count"></a>最大項目計數
查詢，hello 值`MaxItemCount`可以端對端查詢時間有重大影響。 每個往返 toohello 伺服器將會傳回多項目中的 hello 數目`MaxItemCount`（預設值是 100 個項目）。 設定此 tooa 較高的值 （-1 是最大和建議使用） 會由限制 hello 的往返次數伺服器和用戶端之間，特別是針對大型結果集的查詢來改善整體查詢持續時間。

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>平行處理原則的最大程度
查詢微調 hello `MaxDegreeOfParallelism` tooidentify hello 的最佳組態應用程式，特別是當您執行跨資料分割查詢 （不含篩選的 hello 資料分割索引鍵的值）。 `MaxDegreeOfParallelism`控制 hello 最大的平行工作數，亦即，hello 最多個資料分割 toobe 以平行方式瀏覽。 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

假設
* D = 預設最大數目 （= hello 用戶端機器中的處理器總數） 的平行工作
* P = 使用者指定的平行工作最大數目
* N = 需要瀏覽 toobe 回應查詢的資料分割數目

以下是 p 的各種值 hello 平行查詢會有的行為的影響
* (P == 0) => 序列模式
* (P == 1) => 一項工作的最大值
* (P > 1) => 平行工作的最小值 (P, N) 
* (P < 1) => 平行工作的最小值 (N, D)

如需 SDK 版本資訊，以及所實作類別和方法的詳細資訊，請參閱 [DocumentDB SDK](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>網路延遲
請參閱[Azure Cosmos DB 全域發佈](tutorial-global-distribution-documentdb.md)tooset 如何向上全域發佈，和連接 toohello 最接近的區域。 當您需要多個往返 toomake 或擷取大型結果集從 hello 查詢時，網路延遲會具有重要的影響查詢效能。 

hello 的查詢執行計量一節說明如何 tooretrieve hello 查詢伺服器執行時間 ( `totalExecutionTimeInMs`)，如此您就可以區分查詢執行所花費的時間以及花在網路傳輸過程中時間之間。

### <a name="indexing-policy"></a>編製索引原則
若要了解編製索引路徑、種類和模式，以及它們如何影響執行查詢，請參閱[設定編製索引原則](indexing-policies.md)。 根據預設，hello 編製索引原則使用雜湊索引的字串，也就是有效的等號查詢，但不適用於範圍查詢/訂單的查詢。 如果您需要範圍查詢字串時，我們建議您指定 hello 範圍索引類型的所有字串。 

## <a name="query-execution-metrics"></a>查詢執行計量
您可以取得詳細的度量，於查詢執行傳入 hello 選擇性`x-ms-documentdb-populatequerymetrics`標頭 (`FeedOptions.PopulateQueryMetrics` hello.NET SDK 中)。 hello 中傳回值`x-ms-documentdb-query-metrics`具有下列索引鍵 / 值組是對進階疑難排解的查詢執行的 hello。 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| 計量 | 單位 | 說明 | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | 毫秒 | 查詢執行時間 | 
| `queryCompileTimeInMs` | 毫秒 | 查詢編譯時間  | 
| `queryLogicalPlanBuildTimeInMs` | 毫秒 | 時間 toobuild 邏輯的查詢計劃 | 
| `queryPhysicalPlanBuildTimeInMs` | 毫秒 | 時間 toobuild 實體的查詢計劃 | 
| `queryOptimizationTimeInMs` | 毫秒 | 最佳化查詢所花費的時間 | 
| `VMExecutionTimeInMs` | 毫秒 | 查詢執行階段所花費的時間 | 
| `indexLookupTimeInMs` | 毫秒 | 實體索引層內所花費的時間 | 
| `documentLoadTimeInMs` | 毫秒 | 載入文件所花費的時間  | 
| `systemFunctionExecuteTimeInMs` | 毫秒 | 執行系統 (內建) 函式所花費的總時間，以毫秒為單位  | 
| `userFunctionExecuteTimeInMs` | 毫秒 | 執行使用者定義函式所花費的總時間，以毫秒為單位 | 
| `retrievedDocumentCount` | 毫秒 | 擷取的文件總數  | 
| `retrievedDocumentSize` | 位元組 | 擷取的文件大小總計，以位元組為單位  | 
| `outputDocumentCount` | 計數 | 輸出文件數目 | 
| `writeOutputTimeInMs` | 毫秒 | 查詢執行時間，以毫秒為單位 | 
| `indexUtilizationRatio` | 比率 (<=1) | Hello 篩選 toohello 編號的文件載入所比對文件數目的比率  | 

hello 用戶端 Sdk 可能在內部進行多個查詢作業 tooserve hello 查詢內每個資料分割。 hello 用戶端進行多個呼叫每個資料分割如果 hello 總結果超過`x-ms-max-item-count`，如果 hello 查詢超過 hello 佈建的輸送量為 hello 磁碟分割，或如果 hello 查詢裝載達到 hello 的大小上限每一頁，或如果 hello 查詢達到 hello系統配置的逾時限制。 每個部分查詢執行都會傳回該頁面的 `x-ms-documentdb-query-metrics`。 

以下是一些範例查詢，以及如何 toointerpret hello 度量的某些傳回執行查詢： 

| 查詢 | 範例計量 | 說明 | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | hello 擷取的文件數目是 100 + 1 toomatch hello TOP 子句。 查詢時間大部分花費在 `WriteOutputTime` 和 `DocumentLoadTime`，因為它是一次掃描。 | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount 現在是更高版本 （500 + 1 toomatch hello TOP 子句）。 | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | 在 IndexLookupTime 中大約花費了 0.9 毫秒進行索引鍵查閱，因為它會透過 `/N/?` 進行索引查閱。 | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | 在範圍索引中，於 IndexLookupTime 中所花費的時間稍微多一點 (1.7 毫秒)，因為它會根據 `/N/?` 進行索引查閱。 | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | 在 `DocumentLoadTime` 上所花費的時間與上一個查詢相同，但 `WriteOutputTime` 較低，因為我們只要投影一個屬性。 | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | 關於 213 ms 花費在`UserDefinedFunctionExecutionTime`執行上的每個值 hello UDF `c.N`。 |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | 在 `IndexLookupTime` 中針對 `/Name/?` 大約花費了 0.6 毫秒。 大部分的 hello 查詢中的執行時間 （~ 7 毫秒） `SystemFunctionExecutionTime`。 |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | 查詢會當作掃描來執行，因為它使用 `LOWER`，而且會傳回 2491 份擷取文件中的 500 份。 |


## <a name="next-steps"></a>後續步驟
* toolearn 有關 hello 支援 SQL 查詢運算子和關鍵字，請參閱[SQL 查詢](documentdb-sql-query.md)。 
* toolearn 需要求單位，請參閱[要求單位](request-units.md)。
* toolearn 有關編製索引原則，請參閱[編製索引原則](indexing-policies.md) 


