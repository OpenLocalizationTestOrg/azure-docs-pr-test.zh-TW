---
title: "hello 變更 aaaWorking 摘要支援在 Azure Cosmos DB |Microsoft 文件"
description: "使用 Azure Cosmos DB 變更摘要的支援 tootrack 變更文件中，與執行以事件為基礎的處理，例如觸發程序及保持最新狀態的快取和分析系統。"
keywords: "變更摘要"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>使用在 Azure Cosmos DB hello 變更摘要支援
[Azure Cosmos DB](../cosmos-db/introduction.md) 是一項快速且有彈性的全域複製資料庫服務，可用來儲存大量的交易式和操作資料，且具有可預測的讀取和寫入個位數毫秒延遲。 這使得它適合用於 IoT、遊戲、零售，以及操作記錄應用程式。 這些應用程式中的一般設計模式是 tootrack 變更進行 tooAzure Cosmos DB 的資料，並更新具體化的檢視，根據這些變更的特定事件上執行即時分析、 封存資料 toocold 存放裝置及觸發通知。 hello**變更摘要支援**Azure Cosmos DB 可讓您在 toobuild 有效率且可擴充的解決方案為每個這些模式。

變更摘要的支援，Azure Cosmos DB 會提供 Azure Cosmos DB 中的集合已修改它們的 hello 順序中的文件的已排序的清單。 此摘要可以修改 toodata hello 集合內的使用的 toolisten 和執行下列動作：

* 插入或修改文件時，觸發程序呼叫 tooan 應用程式開發介面
* 執行即時 (串流) 更新處理
* 與快取、搜尋引擎或資料倉儲進行資料同步處理

Azure Cosmos DB 中的變更會加以保存，且可進行非同步處理，並分散到一或多個取用者以進行平行處理。 讓我們看看 hello 應用程式開發介面的變更摘要，並且您可以如何使用這些 toobuild 可擴充的即時應用程式。 本文示範如何搭配 Azure Cosmos DB toowork 變更摘要 」 和 「 hello DocumentDB API。 

![使用 Azure Cosmos DB 變更摘要 toopower 即時分析和事件導向運算的案例](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> 變更摘要支援僅提供 hello DocumentDB API 在這個階段中。hello Graph API 和資料表 API 目前不支援。

## <a name="use-cases-and-scenarios"></a>使用個案和案例
變更摘要可有效處理大型資料集有大量的寫入時，可讓，並提供替代 tooquerying 整個資料集 tooidentify 有什麼變更。 比方說，您可以執行下列工作有效率地 hello:

* 透過儲存在 Azure Cosmos DB 中的資料，來更新快取、搜尋索引或資料倉儲。
* 實作階層處理和封存的應用程式層級資料，也就是儲存在 Azure Cosmos DB 中，「 熱資料 」，並且太到期 「 冷資料 」[Azure Blob 儲存體](../storage/common/storage-introduction.md)或[Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)。
* 使用 [Apache Hadoop](run-hadoop-with-hdinsight.md) 在資料上實作批次分析。
* 透過 Azure Cosmos DB [在 Azure 上實作 Lambda 管線 (英文)](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/)。 Azure Cosmos DB 提供一個可調整的資料庫解決方案，可以處理擷取和查詢，並實作具有低 TCO 的 Lambda 架構。 
* 執行零停機時間移轉 tooanother Azure Cosmos DB 帳戶不同的資料分割配置。

**搭配 Azure Cosmos DB 使用 Lambda 管線進行擷取和查詢：**

![適用於擷取和查詢的 Azure Cosmos DB 型 Lambda 管線](./media/change-feed/lambda.png)

您可以使用 Azure Cosmos DB tooreceive 和儲存事件資料，從裝置、 感應器、 基礎結構和應用程式，並處理這些事件與即時[Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md)， [Apache Storm](../hdinsight/hdinsight-storm-overview.md)，或[Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md)。 

在您[無伺服器](http://azure.com/serverless)web 和行動裝置應用程式，您可以追蹤事件，例如變更 tooyour 客戶的設定檔、 喜好設定或位置 tootrigger 特定動作，如傳送推播通知 tootheir 裝置使用[Azure 函數](../azure-functions/functions-bindings-documentdb.md)或[應用程式服務](https://azure.microsoft.com/services/app-service/)。 如果您使用 Azure Cosmos DB toobuild 遊戲，比方說，您可以使用變更摘要的 tooimplement 即時排行榜根據從已完成的遊戲的分數。

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>變更摘要在 Azure Cosmos DB 中的運作方式
Azure 的 Cosmos DB 會提供 hello 能力 tooincrementally 讀取所做的更新 tooan Azure Cosmos DB 集合。 此變更摘要具有下列屬性的 hello:

* 變更會在 Azure Cosmos DB 中持續保存，並且可以非同步處理。
* 在集合中的變更 toodocuments 可立即用於 hello 變更摘要。
* 每個變更 tooa 文件會出現一次在 hello 變更的摘要，以及用戶端管理其檢查點的邏輯。 hello 變更摘要的處理器程式庫會提供自動檢查點和 「 至少一次 」 語意。
* 唯一 hello 最新變更給定文件包含在 hello 變更記錄檔中。 中繼變更可能無法使用。
* hello 變更摘要 （依照修改內每個資料分割索引鍵值的順序） 排序。 跨資料分割索引鍵值順序不會是固定的。
* 變更可以從任何時間點同步處理，也就是說，可用變更沒有固定的資料保留期限。
* 變更會以資料分割索引鍵區塊為單位提供。 這項功能可讓大型集合 toobe 平行處理多個取用者/伺服器的變更。
* 應用程式可以要求多個變更的摘要同時 hello 相同的集合。

根據預設，所有帳戶都會啟用 Azure Cosmos DB 的變更摘要。 您可以使用您[佈建的輸送量](request-units.md)中寫入區域或任何[讀取區域](distribute-data-globally.md)tooread hello 從變更的摘要，就像任何其他作業，從 Azure Cosmos DB。 hello 變更摘要會包含插入和更新作業進行 toodocuments hello 集合內。 您可以擷取刪除項目，方法是在您的文件內設定「虛刪除」旗標來取代刪除動作。 或者，您可以設定您的文件，透過 hello 有限的逾期期限[TTL 功能](time-to-live.md)，例如，24 小時和使用 hello 值 toocapture 刪除該屬性。 此解決方案中，您可以 tooprocess 變更比 hello TTL 到期期限內存留較短的時間間隔內。 hello 變更摘要供在 hello 文件集合中，每個資料分割索引鍵範圍，因此可以分散安裝在平行處理的一或多個取用者。 

![Azure Cosmos DB 變更摘要的分散式處理](./media/change-feed/changefeedvisual.png)

關於如何在用戶端程式碼中實作變更摘要，我們提供了幾個選項給您。 hello 區段，請立即遵循說明 tooimplement hello 使用 hello Azure Cosmos DB REST API 的變更摘要的方式，和 hello DocumentDB Sdk。 不過，.NET 應用程式，我們建議您使用 hello 新[變更摘要處理器庫](#change-feed-processor)簡化資料分割的讀取變更，並可讓多個執行緒使用，處理事件從 hello 變更摘要平行。 

## <a id="rest-apis"></a>使用 REST API 和 DocumentDB Sdk hello
Azure Cosmos DB 提供彈性的儲存體及輸送量容器，稱為**集合**。 集合內的資料會針對延展性和效能，使用[資料分割索引鍵](partition-data.md)以邏輯方式分組。 Azure Cosmos DB 提供各種用來存取此資料的 API，包括依識別碼查閱 (Read/Get)、查詢及讀取摘要 (掃描)。 hello 變更摘要，可取得擴展兩個新的要求標頭 toohello DocumentDB`ReadDocumentFeed`應用程式開發介面，而且跨越的資料分割索引鍵範圍以平行方式處理。

### <a name="readdocumentfeed-api"></a>ReadDocumentFeed API
讓我們快速看一下 ReadDocumentFeed 的運作方式。 Azure Cosmos DB 支援讀取透過 hello 集合內的文件的摘要`ReadDocumentFeed`應用程式開發介面。 例如，hello 下列要求會傳回文件內部 hello 頁面`serverlogs`集合。 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

結果會受到使用 hello`x-ms-max-item-count`由重新送出 hello 要求，則可以繼續標頭，並且讀取`x-ms-continuation`hello 前一個回應中傳回的標頭。 當從單一用戶端執行時，`ReadDocumentFeed` 會以序列方式逐一查看資料分割之間的結果。 

**序列讀取文件摘要**

您也可以擷取的文件使用其中一種支援的 hello hello 摘要[Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)。 例如，下列程式碼片段說明如何 hello toouse hello [ReadDocumentFeedAsync 方法](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet).NET 中。

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>ReadDocumentFeed 的分散式執行
針對包含數 TB 以上資料或需內嵌大量更新的集合，序列執行單一用戶端電腦的讀取摘要可能不夠實際。 在訂單 toosupport 這些巨量資料案例中，Azure Cosmos DB 也提供 Api toodistribute`ReadDocumentFeed`無障礙地跨多個用戶端讀取器/取用者呼叫。 

**分散式讀取文件摘要**

累加變更，Azure Cosmos DB tooprovide 可擴充處理 hello 變更摘要的資料分割索引鍵範圍為基礎的應用程式開發介面支援向外延展模型。

* 您可以針對執行 `ReadPartitionKeyRanges` 呼叫的集合取得資料分割索引鍵範圍的清單。 
* 對於每個資料分割索引鍵範圍，您可以執行`ReadDocumentFeed`tooread 該範圍內的資料分割索引鍵的文件。

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>擷取集合的資料分割索引鍵範圍
您可以擷取要求的 hello hello 資料分割索引鍵範圍`pkranges`集合中的資源。 例如 hello 下列要求會擷取 hello 份資料分割索引鍵範圍 hello`serverlogs`集合：

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

此要求會傳回下列回應包含 hello 資料分割索引鍵範圍的相關中繼資料的 hello:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**資料分割索引鍵範圍屬性**： 每個資料分割索引鍵範圍 hello 中繼資料中包含下表中的 hello:

<table>
    <tr>
        <th>標頭名稱</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>hello 識別碼 hello 資料分割索引鍵範圍。 這是每個集合內穩定且唯的一識別碼。</p>
            <p>必須使用下列呼叫 tooread 變更 hello 中資料分割索引鍵範圍。</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>hello 最大的磁碟分割 hello 資料分割索引鍵範圍的索引鍵的雜湊值。 供內部使用。</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>hello 最小分割區 hello 資料分割索引鍵範圍的索引鍵的雜湊值。 供內部使用。</td>
    </tr>       
</table>

您可以使用其中一種支援的 hello [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)。 比方說，hello 下列程式碼片段示範如何 tooretrieve 資料分割索引鍵範圍在.NET 中使用 hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet)方法。

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Azure Cosmos DB 支援擷取的每個資料分割索引鍵範圍的文件的選擇性設定 hello`x-ms-documentdb-partitionkeyrangeid`標頭。 

### <a name="performing-an-incremental-readdocumentfeed"></a>執行累加式 ReadDocumentFeed
ReadDocumentFeed 支援下列案例/工作的 Azure Cosmos DB 集合中的變更累加處理 hello:

* 讀取所有變更 toodocuments 從 hello 開頭，也就是從集合建立。
* 讀取所有變更 toofuture 更新 toodocuments 從目前的時間或任何變更，因為使用者指定的時間。
* 讀取所有變更 toodocuments hello 集合 (ETag) 的邏輯版本。 您可以根據 hello 累加讀取摘要要求所傳回的 ETag 的取用者的檢查點。

hello 變更包括 toodocuments 插入和更新。 toocapture 刪除，您必須使用在文件中的 「 虛刪除 」 的屬性，或使用 hello[內建的 TTL 屬性](time-to-live.md)toosignal hello 暫止刪除動作變更摘要。

下列表格列出 hello hello[要求](/rest/api/documentdb/common-documentdb-rest-request-headers.md)和[回應標頭](/rest/api/documentdb/common-documentdb-rest-response-headers.md)ReadDocumentFeed 作業。

**累加式 ReadDocumentFeed 的要求標頭**：

<table>
    <tr>
        <th>標頭名稱</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>必須設定太"Incremental 摘要 」，或省略</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>沒有標頭： 從 hello 開頭 （建立集合） 會傳回所有變更</p>
            <p>"*": 傳回 hello 集合內的所有新變更 toodata</p>         
            <p>&lt;etag&gt;： 如果設定 tooa 集合 ETag，會傳回所有的邏輯時間戳記之後所做的變更</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>RFC 1123 時間格式；如果已指定 If-None-Match，則忽略</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>讀取資料的資料分割索引鍵範圍識別碼 hello。</td>
    </tr>
</table>

**累加式 ReadDocumentFeed 的回應標頭**：

<table> <tr>
        <th>標頭名稱</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>hello 邏輯序號 (LSN) 的最後一個 hello 回應中傳回的文件。</p>
            <p>透過在 If-None-Match 中重新提交此值，可以繼續執行累加式 ReadDocumentFeed。</p>
        </td>
    </tr>
</table>

以下是範例要求 tooreturn hello 邏輯版本/ETag 從集合中的所有增量變更`28535`和資料分割索引鍵範圍 = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

變更會依據排序內每個資料分割索引鍵值 hello 資料分割索引鍵範圍內的時間。 跨資料分割索引鍵值順序不會是固定的。 如果有超過可在單一頁面中容納更多結果，您可以重新提交具有以 hello hello 要求讀取下一頁結果 hello`If-None-Match`標頭的值等於 toohello`etag`從 hello 前一個回應。 如果多個文件插入或更新預存程序或觸發程序內的交易，它們將全部傳回 hello 內相同的回應頁面。

> [!NOTE]
> 使用變更的摘要，您可能會收到多個項目中所指定，在頁面中傳回`x-ms-max-item-count`在 hello 案例中的多個文件中插入或更新預存程序或觸發程序。 

Hello.NET SDK (1.17.0) 時，設定 hello 欄位`StartTime`中`ChangeFeedOptions`toodirectly 傳回變更後的文件`StartTime`呼叫時`CreateDocumentChangeFeedQuery`。 藉由指定`If-Modified-Since`使用 hello REST API，您的要求會傳回不 hello 文件，本身，但而 hello 接續 token 或`etag`hello 回應標頭中。 修改過的 hello 指定 hello 接續 token 的時間之 tooreturn hello 文件`etag`然後必須使用與 hello 下一次要求`If-None-Match`tooreturn hello 實際文件。 

hello.NET SDK 提供 hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet)和[ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper 類別 tooaccess 變更 tooa 集合。 hello 下列程式碼片段示範如何 tooretrieve 所有變更從 hello 開頭使用從單一用戶端 hello.NET SDK。

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
Hello 下列程式碼片段示範如何 tooprocess 變更即時和搭配使用 hello 變更 Azure Cosmos DB 摘要支援和 hello 前面函式。 hello 第一次呼叫 hello 集合中傳回所有 hello 文件，hello 第二個只會都傳回 hello 兩份文件建立 hello 最後一個檢查點之後所建立。

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

您也可以篩選 hello 使用用戶端邏輯 tooselectively 程序事件的變更摘要。 例如，以下是使用用戶端端 LINQ tooprocess 僅溫度變更事件，從裝置感應器的程式碼片段。

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>變更摘要處理器程式庫
另一個選項是 toouse hello [Azure Cosmos DB 變更摘要處理器文件庫](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed)，這可以幫助您輕鬆地分散處理從摘要跨多個取用者的變更的事件。 hello 程式庫適合用來建置摘要讀取器 hello.NET 平台上的變更。 透過使用包含在 hello hello 方法 hello 變更摘要處理器文件庫會簡化某些工作流程其他 Cosmos DB Sdk 包括： 

* 當資料儲存在多個分割區時，提取變更摘要的更新
* 移動，或從一個集合 tooanother 複寫資料
* 平行執行的更新 toodata 所觸發的動作和摘要的變更 

雖然使用 hello Cosmos Sdk 中的 hello Api 提供精確的存取 toochange 摘要更新每個資料分割中，使用 hello 變更摘要處理器文件庫簡化讀取變更資料分割和多個平行運作的執行緒。 而不是以手動方式讀取每個容器中的變更並儲存每個資料分割的接續 token，hello 變更摘要處理器會自動管理讀取變更資料分割使用租用機制。

hello 程式庫是以 NuGet 套件形式提供： [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)來源為 Github 的程式碼往來[範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)。 

### <a name="understanding-change-feed-processor-library"></a>了解變更摘要處理器程式庫 

有四個主要元件實作 hello 變更摘要的處理器： hello 監視集合、 hello 租用集合、 hello 處理器主機和 hello 取用者。 

**受監視的集合：** hello 監視集合已 hello 資料產生哪些 hello 變更摘要。 任何插入和變更 toohello 監視集合會反映在 hello 集合的 hello 變更摘要。 

**租用集合：** hello 租用集合座標處理 hello 變更摘要跨多個背景工作。 個別集合是一個租用，每個資料分割使用的 toostore hello 租用。 在不同的帳戶以 hello 這個租用集合寫入區域變更摘要的處理器執行接近 toowhere hello 有利 toostore 它。 租用物件包含下列屬性的 hello: 
* 擁有者： 指定擁有 hello 租用 hello 主機
* 接續： 指定在 hello 變更特定資料分割摘要 hello 位置 (接續 token)
* 時間戳記： 上次更新租用。hello 時間戳記會使用的 toocheck 無論 hello 租用會視為已過期 

**處理器的主機：**多少資料分割 tooprocess 根據多少的主控件的執行個體有作用中租用時，決定每一部主機。 
1.  主應用程式啟動時，它會取得所有主機之間的租用 toobalance hello 工作負載。 主機會定期更新租用，以便讓租用保持作用中狀態。 
2.  主機的檢查點 hello 最後一個接續權杖 tooits 租用每個讀取。 tooensure 並行安全，主機就會檢查每個租用更新 hello ETag。 主機也支援其他檢查點策略。  
3.  在關機，主機會釋出所有租用，但保留 hello 接續資訊，因此它可以繼續讀取 hello 預存的檢查點之後。 

在此階段 hello 主機數目不能大於 hello 資料分割 （租用） 的數目。

**取用者：**取用者或背景工作，是指執行 hello 變更摘要處理每個主機所起始的執行緒。 每個處理器主機都可以有多個取用者。 每一個取用者讀取 hello 變更摘要 hello 從磁碟分割指派 tooand 通知其主機的變更和過期租用。

toofurther 了解這些四個元素的變更摘要處理器如何一起運作，讓我們看看下列圖表中的 hello 範例。 hello 監視集合存放區文件，而且使用 hello"city"hello 資料分割索引鍵。 我們看到藍色 hello 分割區包含從"A E"hello"city"欄位的文件，依此類推。 有兩部主機，每個都有兩個取用者從 hello 四個資料分割，以平行方式讀取。 hello 箭號顯示 hello 取用者讀取 hello 中的特定點變更摘要。 Hello 第一個資料分割中 hello 深藍色代表未讀取的變更而 hello 淺藍色代表 hello 已經讀取 hello 變更摘要的變更。 hello 主機使用 hello 租用集合 toostore 「 接續 」 值 tookeep 追蹤記錄的 hello 目前讀取每一個取用者的位置。 

![使用 hello Azure Cosmos DB 變更摘要處理器主機](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>使用變更摘要處理器程式庫 
hello 下列章節說明如何 toouse hello 變更複寫來源集合 tooa 目的地集合中的 hello 內容中的變更摘要處理器文件庫。 此處 hello 來源集合是 hello 監視集合中變更摘要的處理器。 

**安裝並包含 hello 變更摘要處理器 NuGet 封裝** 

在安裝變更摘要處理器 NuGet 套件之前，請先安裝： 
* Microsoft.Azure.DocumentDB 1.13.1 版或更新版本 
* Newtonsoft.Json 9.0.1 版或更新版本 安裝 `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` 並將它納入以作為參考。

**建立受監視的租用集合和目的地集合** 

Hello 租用集合順序 toouse hello 變更摘要處理器文件庫，必須 toobe 建立之前執行 hello 處理器的主機。 同樣地，我們建議將租用集合儲存在不同的帳戶以寫入區域更接近 toowhere hello 變更摘要處理器正在執行。 資料移動在本例中，我們需要 toocreate hello 目的集合，然後再執行 hello 變更摘要處理器的主機。 在 hello 範例程式碼中，我們稱監視，協助程式方法 toocreate hello 租用，和如果它們尚不存在的目的集合。 

> [!WARNING]
> 建立集合的定價顧慮，為您保留 Azure Cosmos db hello 應用程式 toocommunicate 的輸送量。 如需詳細資訊，請瀏覽 hello[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

建立處理器主機

hello`ChangeFeedProcessorHost`類別會提供安全執行緒、 多處理序、 安全的執行階段環境來實作事件處理器，也提供檢查點檢查與資料分割租用管理。 toouse hello`ChangeFeedProcessorHost`類別時，您可以實作`IChangeFeedObserver`。 這個介面包含三個方法：

* `OpenAsync`：當變更摘要觀察者開啟時，系統就會呼叫這個函式。 取用者/觀察者開啟時，它可以是修改的 tooperform 特定動作。  
* `CloseAsync`：當變更摘要觀察者終止時，系統就會呼叫這個函式。 取用者/觀察者關閉時，它可以是修改的 tooperform 特定動作。  
* `ProcessChangesAsync`：當變更摘要有新的文件變更時，系統就會呼叫這個函式。 它可以是修改的 tooperform 每個摘要的變更更新時的特定動作。  

在本例中，我們會實作 hello 介面`IChangeFeedObserver`透過 hello`DocumentFeedObserver`類別。 在這裡，hello`ProcessChangesAsync`函式從變更的文件送入 hello 目的地集合 upserts （更新）。 這個範例可用於將資料從一個集合 tooanother 中順序 toochange hello 資料分割索引鍵的資料集。 

*執行 hello 處理器主機*

在開始事件的處理之前，您可以自訂變更摘要選項和變更摘要主機選項。 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
在 hello 下表摘要說明 hello 可自訂的特定欄位。 

**變更摘要選項**：
<table>
    <tr>
        <th>屬性名稱</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>取得或設定 hello hello Azure Cosmos DB 資料庫服務中的 hello 列舉作業傳回的項目 toobe 數目上限。</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>取得或設定在 hello Azure Cosmos DB 資料庫服務的 hello hello 目前要求的資料分割索引鍵範圍識別碼。</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>取得或設定在 hello Azure Cosmos DB 資料庫服務的 hello 要求接續 token。</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>取得或設定與 hello Azure Cosmos DB 資料庫服務的工作階段一致性 hello 工作階段語彙基元供使用。</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>取得或設定是否從 hello 開頭 (true) 或目前 (false)，應該啟動摘要 hello Azure Cosmos DB 資料庫服務中的變更。 根據預設，它會從目前位置 (false) 來開始。</td>
    </tr>
</table>

**變更摘要主機選項**:
<table>
    <tr>
        <th>屬性名稱</th>
        <th>類型</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>時間範圍</td>
        <td>hello 的間隔時間的所有租用目前 hello ChangeFeedEventHost 執行個體所持有的資料分割。</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>時間範圍</td>
        <td>資料分割，平均分散在已知的主控件執行個體是否 hello 間隔 tookick 工作 toocompute 關閉。</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>時間範圍</td>
        <td>代表資料分割在租用期租用會執行哪些 hello 的 hello 間隔。 在此時間間隔內未更新 hello 租用後，如果它已過期，而且 hello 分割區的擁有權移 tooanother ChangeFeedEventHost 執行個體。</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>時間範圍</td>
        <td>之後即會清空所有目前的變更摘要 hello 輪詢 hello 上的新變更的資料分割之間的延遲。</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>hello 頻率 toocheckpoint 租用。</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>hello hello 主機的最小分割區計數。</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>可以做 hello 分割 hello 主機的數目上限。</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Bool</td>
        <td>應該刪除是否 hello 上啟動 hello 主機的所有現有的租用和 hello 主機應該從頭開始。</td>
    </tr>
</table>


toostart 事件處理，具現化`ChangeFeedProcessorHost`，提供 Azure Cosmos DB 集合中的 hello 適當的參數。 然後，呼叫`RegisterObserverAsync`tooregister 您`IChangeFeedObserver`hello 執行階段 (在此範例中 DocumentFeedObserver) 實作。 此時，hello 主機嘗試 tooacquire 使用 「 窮盡 」 演算法 hello Azure Cosmos DB 集合中每個資料分割索引鍵範圍上的租用。 這些租用會延續一段指定時間，然後必須更新。 為新的節點，背景工作執行個體，在此情況下，上線，它們會預訂租約，並且經過一段時間 hello 負載會轉移節點之間為每一部主機嘗試次數 tooacquire 更多租用。 

在 hello 範例程式碼，我們使用處理站類別 (DocumentFeedObserverFactory.cs) toocreate 觀察者和 hello `RegistObserverFactoryAsync` tooregister hello 觀察者。 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
經過一段時間後，均衡的局面將會出現。 此動態功能可讓 CPU 型自動調整套用 toobe tooconsumers 向上延展和向下調整。 變更有更快的速度比處理取用者可以提供 Azure Cosmos DB，取用者上的 hello CPU 增加可以使用的 toocause 自動調整規模上背景工作執行個體計數。

## <a name="next-steps"></a>後續步驟
* 再試一次 hello [Azure Cosmos 資料庫變更摘要 GitHub 上的程式碼範例](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* 開始撰寫程式碼以 hello [Azure Cosmos DB Sdk](documentdb-sdk-dotnet.md)或 hello [REST API](/rest/api/documentdb/)。
