---
title: "Azure Cosmos DB: 使用 DocumentDB API 在.NET 中的 hello 開發 |Microsoft 文件"
description: "深入了解如何使用適用於.NET 的 Azure Cosmos DB 的 DocumentDB api toodevelop"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>使用 DocumentDB API 在.NET 中的 hello 開發 azure CosmosDB:

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本教學課程示範如何 toocreate Azure Cosmos DB 帳戶使用 hello Azure 入口網站，並接著建立文件資料庫和集合[資料分割索引鍵](documentdb-partition-data.md#partition-keys)使用 hello [DocumentDB.NET API](documentdb-introduction.md)。 藉由定義資料分割索引鍵，當您建立集合時，您的應用程式已準備好 tooscale 毫不費力地隨著您的資料。 

此教學課程涵蓋 hello 下列工作使用 hello [DocumentDB.NET API](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * 建立 Azure Cosmos DB 帳戶
> * 建立具有分割區索引鍵的資料庫和集合
> * 建立 JSON 文件
> * 更新文件
> * 查詢已分割的集合
> * 執行預存程序
> * 刪除文件
> * 刪除資料庫

## <a name="prerequisites"></a>必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/free/)。 
    * 或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程，如果您想要 toouse 本機模擬的環境，供開發應用程式的 hello Azure DocumentDB 服務。
* [Visual Studio](http://www.visualstudio.com/)。

## <a name="create-an-azure-cosmos-db-account"></a>建立 Azure Cosmos DB 帳戶

首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。

> [!TIP]
> * 已經有 Azure Cosmos DB 帳戶？ 如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)
> * 您是否已有 Azure DocumentDB 帳戶？ 如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。  
> * 如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>設定您的 Visual Studio 方案
1. 在電腦上開啟 **Visual Studio**。
2. 在 hello**檔案**功能表上，選取**新增**，然後選擇 **專案**。
3. 在 hello**新專案**對話方塊中，選取**範本** / **Visual C#** / **主控台應用程式 (.NET Framework)**，命名您的專案，然後按一下**確定**。
   ![Hello 新增專案 視窗的螢幕擷取畫面](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. 在 [hello**方案總管] 中**，新主控台應用程式，也就是在您的 Visual Studio 方案，以滑鼠右鍵按一下，然後按一下**管理 NuGet 封裝...**
    
    ![螢幕擷取畫面的權限 hello hello 專案的已按下功能表](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. 在 hello **NuGet**索引標籤上，按一下 **瀏覽**，然後輸入**documentdb** hello 搜尋 方塊中。
<!---stopped here--->
6. 在 hello 結果中尋找**Microsoft.Azure.DocumentDB**按一下**安裝**。
   hello 封裝識別碼 hello Azure Cosmos DB 用戶端程式庫是[Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)。
   ![尋找 Azure Cosmos DB 用戶端 SDK 的 NuGet 功能表 hello 的螢幕擷取畫面](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    如果您收到有關檢閱變更 toohello 方案，請按一下**確定**。 如果您收到關於接受授權的訊息，請按一下 [我接受]。

## <a id="Connect"></a>加入參考 tooyour 專案
中這個教學課程提供 hello DocumentDB API 的程式碼片段所需 toocreate 和更新 Azure Cosmos DB 資源專案中的 hello 剩餘步驟。

首先，新增這些參考 tooyour 應用程式。
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>連接您的應用程式

接著，在應用程式中新增下列兩個常數和您的「用戶端」變數。

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

標頭然後回 toohello [Azure 入口網站](https://portal.azure.com)tooretrieve 您的端點 URL 和主索引鍵。 hello 端點 URL 及主要金鑰所需的應用程式 toounderstand 位置，以及 Azure Cosmos DB tootrust tooconnect 應用程式的連接。

在 hello Azure 入口網站，瀏覽 tooyour Azure Cosmos DB 帳戶，按一下 **金鑰**，然後按一下**讀寫金鑰**。

從 hello 入口網站複製 hello URI，並將它貼入`<your endpoint URL>`hello program.cs 檔案中。 複製 hello 從 hello 入口網站的主索引鍵，並將它貼入`<your primary key>`。 要確定 tooremove hello`<`和`>`從您的值。

![Hello Azure 入口網站的螢幕擷取畫面 hello NoSQL 教學課程 toocreate 使用 C# 主控台應用程式。 顯示 Azure Cosmos DB 帳戶，hello 上 hello Azure Cosmos DB 帳戶刀鋒視窗中，反白顯示的索引鍵和 hello URI 與主索引鍵 hello 金鑰刀鋒視窗上反白顯示的值](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>具現化 hello DocumentClient

現在，建立新的執行個體的 hello **DocumentClient**。

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>建立資料庫

接下來，建立 Azure Cosmos DB[資料庫](documentdb-resources.md#databases)使用 hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx)方法或[CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx)方法 hello **DocumentClient**類別從 hello [DocumentDB.NET SDK](documentdb-sdk-dotnet.md)。 資料庫是 hello 的 JSON 文件儲存分割於各個集合的邏輯容器。

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>選定分割區索引鍵 

集合是用來儲存文件的容器。 它們是邏輯資源，並且可以[跨一或多個實體分割區](partition-data.md)。 A[資料分割索引鍵](documentdb-partition-data.md)是屬性 （或路徑） 內所使用的 toodistribute 文件之間 hello 伺服器或資料分割資料。 所有文件以 hello 相同的資料分割索引鍵會儲存在 hello 相同的資料分割。 

決定資料分割索引鍵是重要的決策 toomake 之前建立的集合。 資料分割索引鍵屬性 （或路徑） 都可以是您的文件中使用 Azure Cosmos DB toodistribute 您在多個伺服器或資料分割之間的資料。 Cosmos DB hello 資料分割索引鍵值的雜湊，並使用哪些 toostore hello 文件中的雜湊的 hello 結果 toodetermine hello 磁碟分割。 所有文件以 hello 相同的資料分割索引鍵會儲存在 hello 相同的資料分割，並在集合建立後，就無法變更資料分割索引鍵。 

此教學課程中，我們會 tooset hello 資料分割索引鍵太`/deviceId`因此的 hello hello 的所有資料對於單一裝置儲存在單一資料分割中。 您想要 toochoose 具有大量的值，其中每個使用資料分割索引鍵在 hello 關於相同頻率 tooensure Cosmos DB 可以負載平衡資料成長以及達到 hello 全部輸送量，hello 集合。 

如需有關資料分割的詳細資訊，請參閱[如何 toopartition 和小數位數，在 Azure Cosmos DB 嗎？](partition-data.md) 

## <a id="CreateColl"></a>建立集合 

既然我們知道我們的資料分割索引鍵， `/deviceId`，可讓您建立[集合](documentdb-resources.md#collections)使用 hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx)方法或[CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx)方法 hello **DocumentClient**類別。 集合是 JSON 文件和任何相關 JavaScript 應用程式邏輯的容器。 

> [!WARNING]
> 建立集合的定價顧慮，為您保留 Azure Cosmos db hello 應用程式 toocommunicate 的輸送量。 如需更多詳細資料，請瀏覽我們的[定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

這個方法會 REST API 呼叫 tooAzure Cosmos DB 而且 hello 服務佈建的 hello 要求輸送量為基礎的資料分割數目。 您可以變更您的效能需求的發展使用 hello SDK 或 hello 集合中的 hello 輸送量[Azure 入口網站](set-throughput.md)。

## <a id="CreateDoc"></a>建立 JSON 文件
我們將把一些 JSON 文件插入到 Azure Cosmos DB。 A[文件](documentdb-resources.md#documents)可以建立使用 hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx)方法 hello **DocumentClient**類別。 文件會是使用者定義的 (任意) JSON 內容。 此範例類別包含裝置讀取，且呼叫 tooCreateDocumentAsync tooinsert 讀入集合的新裝置。

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a>讀取資料

讓我們來讀取 hello 文件，其資料分割索引鍵並使用 hello ReadDocumentAsync 方法的識別碼。 請注意，hello 讀取包含 PartitionKey 值 (對應 toohello `x-ms-documentdb-partitionkey` hello REST API 中的要求標頭)。

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>更新資料

現在讓我們先更新某些使用 hello ReplaceDocumentAsync 方法的資料。

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>刪除資料

現在可讓使用 hello DeleteDocumentAsync 方法刪除的資料分割索引鍵的文件和識別碼。

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>查詢已分割的集合

當您查詢資料分割的集合，Azure Cosmos DB 中的資料會自動路由 hello 對應 toohello 資料分割索引鍵值 （如果有的話），hello 篩選中指定的查詢 toohello 分割區。 例如，此查詢是路由的 toojust hello 磁碟分割包含 hello 資料分割索引鍵"XMS 0001"。

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
hello 下列查詢 hello 資料分割索引鍵 (DeviceId) 上沒有篩選器，視窗成扇形散開 tooall 分割區執行針對 hello 分割區索引。 請注意，您必須 toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` hello REST API 中) toohave hello SDK tooexecute 橫跨資料分割的查詢。

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a>平行查詢執行
hello Azure Cosmos DB DocumentDB Sdk 1.9.0 和上方支援平行查詢執行選項，可讓您 tooperform 低度延遲查詢針對資料分割的集合，即使他們需要 tootouch 大量的資料分割。 比方說，下列查詢的 hello 是以平行方式設定的 toorun 橫跨資料分割。

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
您可以管理執行平行查詢微調 hello 下列參數：

* 藉由設定`MaxDegreeOfParallelism`，您可以控制 hello 程度的平行處理原則即 hello 同時網路連線 toohello 集合的資料分割數目上限。 如果您設定太-1，會將平行處理原則程度 hello 受 hello SDK。 如果 hello`MaxDegreeOfParallelism`未指定或設定 too0，也就是 hello 預設值，會有單一網路連線 toohello 集合的資料分割。
* 您可藉由設定 `MaxBufferedItemCount`，來權衡取捨查詢延遲和用戶端記憶體使用量。 如果您省略這個參數，或將此設定太-1，由 hello SDK 管理 hello 平行查詢執行期間經過緩衝處理的項目數目。

指定 hello hello 集合的相同的州名，平行查詢會傳回結果中 hello 相同排序如同序列執行。 執行包含排序 （ORDER BY 和/或頂端） 的跨資料分割查詢，hello DocumentDB SDK 發出 hello 查詢，以平行方式在資料分割，並將部分已排序的結果，在 hello 用戶端端 tooproduce 全域排序結果。

## <a name="execute-stored-procedures"></a>執行預存程序
最後，您可以執行不可部分完成的交易，對文件以 hello 相同的裝置識別碼，例如： 如果您正在維護彙總，或藉由新增下列程式碼 tooyour 專案 hello hello 單一文件中的裝置最新狀態。

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

就這麼簡單！ 這些是 hello Azure Cosmos DB 應用程式使用資料分割索引鍵 tooefficiently 標尺資料發佈在資料分割之間的主要元件。  

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源，本教學課程以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 唯一名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列： 

> [!div class="checklist"]
> * 建立 Azure Cosmos DB 帳戶
> * 建立具有資料分割索引鍵的資料庫和集合
> * 建立 JSON 文件
> * 更新文件
> * 查詢已分割的集合
> * 執行預存程序
> * 刪除文件
> * 刪除資料庫

您現在可以繼續進行下一個教學課程 toohello 並匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [將資料匯入到 Azure Cosmos DB](import-data.md)
