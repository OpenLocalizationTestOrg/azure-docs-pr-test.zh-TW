---
title: "aaaPartitioning 和 Azure Cosmos DB 中的水平延展 |Microsoft 文件"
description: "了解有關如何分割 Azure Cosmos DB 的運作方式、 如何 tooconfigure 資料分割和資料分割索引鍵，和如何 toopick hello 右資料分割索引鍵應用程式。"
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: cac9a8cd-b5a3-4827-8505-d40bb61b2416
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87d56db8c4ccc6b94b1650baff0fcfb3db6d1777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopartition-and-scale-in-azure-cosmos-db"></a>如何 toopartition 和 Azure Cosmos DB 中的小數位數

[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)是全域的分散式、 多模型資料庫服務，其設計 toohelp 您達成快速、 可預測的效能和擴充順暢地連同應用程式的成長。 本文章提供如何分割適用於所有 hello 資料模型在 Azure Cosmos DB 中，並說明如何設定 Azure Cosmos DB 容器 tooeffectively 延展您的應用程式的概觀。

Scott Hanselman 和 Azure Cosmos DB 工程總經理 Shireesh Thota 也會在這段 Azure Friday 影片中說明資料分割和資料分割索引鍵。

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Azure Cosmos DB 中的資料分割
您在 Azure Cosmos DB 中可儲存及查詢無結構描述的資料，以及任何規模的毫秒順序回應時間。 Cosmos DB 提供存放資料的容器，稱為**集合 (適用於文件)、圖形或資料表**。 容器是邏輯資源，可以跨一或多個實體分割或伺服器。 資料分割的 hello 數目取決於 Cosmos DB hello 儲存體大小和 hello 佈建的輸送量 hello 容器的基礎。 Cosmos DB 中的每個分割都有其相關聯的固定 SSD 支援儲存體數量，並且複寫以提供高可用性。 資料分割管理完全受 Azure Cosmos DB，且您沒有 toowrite 複雜的程式碼或管理您的資料分割。 Cosmos DB 容器在儲存體和輸送量方面並無限制。 

![水平](./media/introduction/azure-cosmos-db-partitioning.png) 

資料分割是透明的 tooyour 應用程式。 Cosmos DB 支援快速讀取和寫入、 查詢、 交易式的邏輯、 一致性層級，以及透過方法/Api tooa 單一容器資源的更細緻的存取控制。 將資料分散到資料分割和路由查詢要求 toohello 正確的資料分割，hello 服務控制代碼。 

資料分割如何運作？ 每個項目必須具備可唯一識別它的資料分割索引鍵和資料列索引鍵。 您的資料分割索引鍵是存放資料的邏輯資料分割區，並為 Cosmos DB 提供將資料分散到分割區的自然界限。 簡單地說，Azure Cosmos DB 中的資料分割運作方式如下︰

* 您使用 `T` 要求/秒的輸送量佈建 Cosmos DB 容器
* Hello 幕後 Cosmos DB 佈建資料分割需要 tooserve`T`要求/秒。 如果`T`高於 hello 每個分割區的最大輸送量`t`，然後佈建 Cosmos DB `N`  =  `T/t`資料分割
* Cosmos DB 配置 hello 金鑰空間的資料分割索引鍵的雜湊平均跨 hello`N`資料分割。 因此，每個分割區 (實體分割區) 會裝載 1-N 個資料分割索引鍵值 (邏輯分割區)
* 當實體資料分割`p`達到其儲存體限制，Cosmos DB 順暢地分割`p`分成兩個新的分割`p1`和`p2`及散發 tooroughly 半 hello 金鑰 tooeach 的 hello 的對應值資料分割。 這個分割作業是不可見的 tooyour 應用程式。
* 同樣地，當您佈建輸送量高於時`t*N`一或多個程式磁碟分割 toosupport hello 較高的輸送量，輸送量，Cosmos DB 分割

資料分割索引鍵的 hello 語意會稍有不同的 toomatch hello 語意的每個 API，hello 下表中所示：

| API | 資料分割索引鍵 | 列索引鍵 |
| --- | --- | --- |
| DocumentDB | 自訂資料分割索引鍵路徑 | 固定 `id` | 
| MongoDB | 自訂共用索引鍵  | 固定 `_id` | 
| 圖形 | 自訂資料分割索引鍵屬性 | 固定 `id` | 
| 資料表 | 固定 `PartitionKey` | 固定 `RowKey` | 

Cosmos DB 使用雜湊型資料分割。 當您撰寫一個項目時，Cosmos DB 雜湊 hello 資料分割索引鍵值，並使用 hello 雜湊結果 toodetermine 中的哪一個資料分割 toostore hello 項目。 所有的項目與 hello 中相同的資料分割索引鍵的 cosmos DB 存放區 hello 相同實體磁碟分割。 hello 選擇 hello 資料分割索引鍵是您在設計階段有 toomake 的重要決策。 您必須選擇具有各種不同的值並且有平均存取模式的屬性名稱。

> [!NOTE]
> 它是最佳的作法 toohave 具有許多相異值 (100年-最少的 1000) 資料分割索引鍵。
>

Azure Cosmos DB 容器可視為「固定」或「無限制」。 固定大小的容器具有上限為 10 GB 和 10,000 RU/秒的輸送量。 某些應用程式開發介面可讓 hello 資料分割索引鍵 toobe 省略的固定大小的容器。 toocreate 為無限制的容器，您必須指定最小 2500 RU/秒的輸送量。

## <a name="partitioning-and-provisioned-throughput"></a>資料分割與佈建的輸送量
Cosmos DB 設計用來取得可預測的效能。 當您建立容器時，可以根據每秒的[要求單位](request-units.md) (RU) 來為每分的 RU 預留輸送量。 每個要求會指派是均衡 toohello 系統資源，例如 CPU、 記憶體和 IO hello 作業所耗用的數量的要求單位費用。 讀取 1 KB 具有工作階段一致性的文件，會使用 1 個要求單位。 讀取為 1 RU 無論 hello 數目的項目儲存或 hello hello 在執行的並行要求數目相同的時間。 較大的項目需要較高的要求單位 hello 大小而定。 如果您知道 hello 大小的實體，並且在 hello 的讀取數 toosupport 需要您的應用程式，您可以佈建 hello 確實所需的應用程式的需要讀取所需的輸送量。 

> [!NOTE]
> tooachieve hello 的輸送量，hello 容器，您必須選擇資料分割索引鍵，可讓您 tooevenly 之間分散要求一些不同的資料分割索引鍵值。
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="working-with-hello-azure-cosmos-db-apis"></a>使用 hello Azure Cosmos DB Api
您可以使用 hello Azure 入口網站或 Azure CLI toocreate 容器，並調整其大小在任何時間。 此區段會顯示如何 toocreate 容器並指定 hello 輸送量和資料分割索引鍵定義中的 hello 的每個支援的 Api。

### <a name="documentdb-api"></a>DocumentDB API
hello 下列範例顯示如何 toocreate 容器 （集合），使用 hello DocumentDB API。 您可以在[使用 DocumentDB API 進行資料分割](partition-data.md)中找到更多詳細資料。

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

您可以讀取項目 （文件） 使用 hello `GET` hello REST API 或使用中的方法`ReadDocumentAsync`其中一種 hello Sdk。

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB API
以 hello MongoDB API，您可以建立分區化的集合，透過您最愛的工具、 驅動程式或 SDK。 在此範例中，我們會使用 hello Mongo 殼層 hello 集合建立的。

在 [hello Mongo 殼層：

```
db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
```
    
結果：

```JSON
{
    "_t" : "ShardCollectionResponse",
    "ok" : 1,
    "collectionsharded" : "admin.people"
}
```

### <a name="table-api"></a>資料表 API

以 hello 表格 API，您指定資料表的 hello 輸送量 hello appSettings 組態中應用程式：

```xml
<configuration>
    <appSettings>
      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
    </appSettings>
</configuration>
```

然後您會建立資料表，使用 hello Azure 資料表儲存體 SDK。 hello 資料分割索引鍵會隱含建立為 hello`PartitionKey`值。 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists();
```

您可以擷取單一實體，使用下列程式碼片段的 hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
請參閱[開發以 hello 表格 API](tutorial-develop-table-dotnet.md)如需詳細資訊。

### <a name="graph-api"></a>圖形 API

以 hello Graph API，您必須使用 hello Azure 入口網站或 CLI toocreate 容器。 或者，由於 Azure Cosmos DB 多模型，您可以使用其中一種 hello 其他模型 toocreate 並調整您的圖形容器。

您可以閱讀任何頂點或使用中 Gremlin hello 資料分割索引鍵和 id 的邊緣。 比方說，圖形與 hello 資料分割索引鍵，以及 「 西雅圖 」 做為 hello 資料列索引鍵的地區 （「 美國 」），您可以找到頂點使用 hello，請使用下列語法：

```
g.V(['USA', 'Seattle'])
```

相同邊緣，您可以參考使用 hello 資料分割索引鍵和資料列索引鍵的邊緣。

```
g.E(['USA', 'I5'])
```

如需詳細資訊，請參閱 [Cosmos DB 的 Gremlin 支援](gremlin-support.md)。


<a name="designing-for-partitioning"></a>
## <a name="designing-for-partitioning"></a>設計資料分割
有效地以 Azure Cosmos DB tooscale，您需要 toopick 良好的資料分割索引鍵，當您建立您的容器。 選擇資料分割索引鍵時有兩個重要考量︰

* **查詢和交易界限**： 您所選擇的資料分割索引鍵應該平衡 hello 需要 tooenable hello 使用的交易，針對 hello 需求 toodistribute 實體之間的多個資料分割索引鍵 tooensure 靈活的解決方案。 其中一種方式，您可以設定 hello 相同的資料分割索引鍵的所有項目，但這可能會限制您的方案 hello 延展性。 在 [hello 其他極端的做法是，您可能會指派唯一的資料分割索引鍵，每個項目，這會具有高擴充性，但會防止使用跨文件交易透過預存程序和觸發程序。 在理想的資料分割索引鍵是其中一個，可讓您 toouse 有效率的查詢，且具有足夠的基數 tooensure 可擴充是您的方案。 
* **任何儲存和效能的瓶頸**： 請務必 toopick 屬性，可讓寫入 toobe 分散到不同的相異值。 要求 toohello 相同的資料分割索引鍵不能超過 hello 輸送量的單一資料分割，而且實行節流措施。 因此，重要 toopick 並不會導致應用程式中的 「 作用點 」 資料分割索引鍵。 自 hello 的所有資料的單一資料分割索引鍵必須儲存在資料分割，也建議具有大量資料的 hello tooavoid 資料分割索引鍵相同的值。 

來看看一些真實案例和每個案例良好的資料分割索引鍵︰
* 如果您正在實作使用者設定檔後端，hello 使用者識別碼會是資料分割索引鍵的理想選擇。
* 如果您在儲存 IoT 資料 (例如，裝置狀態)，則裝置識別碼是不錯的資料分割索引鍵選擇。
* 如果您使用 Azure Cosmos DB 記錄時間序列資料，然後 hello 主機名稱或處理序識別碼是不錯的選擇的資料分割索引鍵。
* 如果您有多租用戶架構，hello 租用戶識別碼會是資料分割索引鍵的理想選擇。

在類似 IoT 和使用者設定檔、 hello 資料分割索引鍵的情況下可能是一些使用 hello 做為 （文件索引鍵） 的識別碼相同。 在其他類似 hello 時間序列資料，您可能必須與 hello 識別碼不同資料分割索引鍵。

### <a name="partitioning-and-loggingtime-series-data"></a>資料分割和記錄/時間序列資料
Cosmos DB 的 hello 常見使用案例是針對記錄與遙測。 它是重要 toopick 良好的資料分割索引鍵，因為您可能需要大量的磁碟區 tooread/寫入的資料。 hello 選擇取決於您的讀取和寫入速率和種類的預期 toorun 的查詢。 以下是一些秘訣 toochoose 良好的資料分割索引鍵。

* 如果您使用案例牽涉到較小的率寫入 [累積一段很長一段時間，以及需要 tooquery 由時間戳記和其他篩選的範圍，則使用彙總套件 hello 時間戳記，例如，日期為資料分割索引鍵是很好的方法。 這可讓您 tooquery 透過 hello 的所有資料針對單一資料分割的日期。 
* 如果您的寫入工作負載繁重 (這是更常見的情形)，則不應該使用根據時間戳記的資料分割索引鍵，這樣一來，Cosmos DB 才可以將寫入工作平均分散到多個資料分割。 在這個案例中，主機名稱、處理序識別碼、活動識別碼或其他具有高基數的屬性是不錯的選擇。 
* 第三種方法是一種混合體一個其中有多個容器，一個用於每日/月 hello 資料分割索引鍵是細微的屬性，例如主機名稱。 此功能還有您可以設定不同的輸送量 hello 時間間隔為基礎的 hello 優點，例如 hello 當月的 hello 容器佈建較高的輸送量因為它是讀取和寫入，而與前的幾個月降低輸送量，因為它們只可讀取。

### <a name="partitioning-and-multi-tenancy"></a>資料分割與多重租用
如果您使用 Cosmos DB 實作多重租用戶應用程式，有兩種常見的模式：一個租用戶一個資料分割索引鍵，和一個租用戶一個容器。 以下是 hello 專業人員以及每個缺點：

* 一個租用戶一個資料分割索引鍵：在此模型中，租用戶共置於單一容器內。 但是，針對單一資料分割，可以執行單一租用戶內項目的查詢與插入。 您也可以跨租用戶內的所有項目實作交易邏輯。 因為多重租用戶共用一個容器，所以您可以節省儲存體和輸送量成本，方法是在單一容器內輪詢租用戶的資源，而不是為每個租用戶佈建額外的空餘空間。 hello 缺點是，您不需要每個租用戶的效能隔離。 效能/輸送量增加套用 toohello 整個容器 vs 目標增加租用戶。
* 一個租用戶一個容器：每個租用戶都有其專屬容器。 在此模型中，您可以保留每個租用戶的效能。 使用 Cosmos DB 全新的佈建計價模式，這種模式對於具有少數租用戶的多重租用戶應用程式最具成本效益。

您也可以使用組合/分層方法可 collocates 小型的租用戶，並移轉較大的租用戶 tootheir 自己的容器。

## <a name="next-steps"></a>後續步驟
在本文中，我們提供使用任一 Azure Cosmos DB API 進行資料分割之概念和最佳做法的概觀。 

* 了解 [Azure Cosmos DB 中佈建的輸送量](request-units.md)
* 了解 [Azure Cosmos DB 中的全域分散](distribute-data-globally.md)



