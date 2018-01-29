---
title: "Azure Cosmos DB 中的資料分割和水平調整 | Microsoft Docs"
description: "了解資料分割在 Azure Cosmos DB 中的運作方式、如何設定資料分割和資料分割索引鍵，以及如何為您的應用程式挑選合適的資料分割索引鍵。"
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
ms.date: 01/05/2018
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0032a00883cedfe754e14293dc13a1009f6dd3a0
ms.sourcegitcommit: 1d423a8954731b0f318240f2fa0262934ff04bd9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="partition-and-scale-in-azure-cosmos-db"></a>在 Azure Cosmos DB 中進行資料分割和調整

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是全域分散的多重模型資料庫服務，其設計可協助您達成快速且可預測的效能。 它會順暢地隨著應用程式的成長而調整規模。 本文概述 Azure Cosmos DB 中所有資料模型的資料分割運作方式的概觀， 並描述可如何設定 Azure Cosmos DB 容器以有效地調整應用程式規模。

Scott Hanselman 和 Azure Cosmos DB 工程總經理 Shireesh Thota 會在這段 Azure Friday 影片中討論資料分割和資料分割索引鍵：

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-DocumentDB-Elastic-Scale-Partitioning/player]
> 

## <a name="partitioning-in-azure-cosmos-db"></a>Azure Cosmos DB 中的資料分割
您在 Azure Cosmos DB 中可儲存及查詢無結構描述的資料，以及任何規模的毫秒順序回應時間。 Azure Cosmos DB 提供存放資料的容器，稱為「集合」(適用於文件)、「圖形」或「資料表」。 

容器是邏輯資源，可以跨一或多個實體分割或伺服器。 資料分割數目取決於 Azure Cosmos DB 的儲存體大小與佈建的容器輸送量。 

實體資料分割是固定保留 SSD 為基礎的存放裝置的數量。 每個實體的資料分割會複寫為高可用性。 一或多個實體的資料分割是由容器所組成。 Azure Cosmos DB，完全管理實體資料分割管理，而且不需要撰寫複雜的程式碼，或管理您的資料分割。 Azure Cosmos DB 容器在儲存體和輸送量方面並無限制。 

邏輯磁碟分割是將單一資料分割索引鍵值相關聯的所有資料都儲存在實體資料分割中的資料分割。 邏輯磁碟分割具有 10 GB 的最大值。下列圖表中，在單一容器會有三個邏輯磁碟分割。 每個邏輯資料分割會分別儲存一個 LAX、 AMS 和 MEL 的資料分割索引鍵的資料。 每個 LAX、 AMS 和 MEL 邏輯磁碟分割無法成長超過最大的邏輯磁碟分割的限制為 10 GB。 

![資源的資料分割](./media/introduction/azure-cosmos-db-partitioning.png) 

當集合符合[分割必要條件](#prerequisites)，資料分割的動作是透明的您的應用程式。 Azure Cosmos DB 支援快速的讀取與寫入、查詢、交易邏輯、一致性層級，以及透過方法/API 對單一容器資源進行更細微的存取控制。 實體和邏輯資料分割之間分散資料，和路由的服務控制代碼查詢正確的資料分割的要求。 

## <a name="how-does-partitioning-work"></a>資料分割的運作方式

資料分割如何運作？ 每個項目必須具備可唯一識別它的資料分割索引鍵和資料列索引鍵。 您的資料分割索引鍵做為資料的邏輯磁碟分割，並提供自然界限的實體資料分割之間分散資料，Azure Cosmos DB。 請注意，單一邏輯資料分割的資料必須位在單一的實體資料分割，但實體資料分割管理受 Azure Cosmos DB。 

簡單地說，Azure Cosmos DB 中的資料分割運作方式如下︰

* 您佈建的 Azure Cosmos DB 容器**T**每第二個輸送量的要求。
* 在幕後，Azure Cosmos DB 佈建服務所需的資料分割**T**每秒要求數。 如果**T**高於每個分割區的最大輸送量**t**，然後佈建 Azure Cosmos DB **N = T/t**資料分割。
* Azure Cosmos DB 配置的資料分割索引鍵的空間索引鍵的雜湊平均透過**N**資料分割。 因此，每個資料分割 （實體磁碟分割） 主機**1/N**資料分割索引鍵的值 （邏輯磁碟分割）。
* 當實體資料分割**p**達到其儲存體限制，Azure Cosmos DB 順暢地分割**p**分成兩個新的資料分割， **p1**和**p2**. 它會分配相當於約索引鍵一半的值給每個分割區。 應用程式不會察覺此分割作業。 如果實體的資料分割已達到儲存體限制，而且所有實體資料分割中的資料屬於相同的邏輯資料分割索引鍵，就不會分割作業。 這是因為單一邏輯資料分割索引鍵的所有資料必須都位於相同的實體磁碟分割，因此您不能在實體資料分割分割為 p1 和 p2。 在此情況下應該採用不同的資料分割索引鍵的策略。
* 當您佈建輸送量高於 **t*N**，Azure Cosmos DB 分割一或多個分割區以支援更高的輸送量。

資料分割索引鍵的語意會稍有不同，以符合各 API 的語意，如下表所示︰

| API | 資料分割索引鍵 | 列索引鍵 |
| --- | --- | --- |
| Azure Cosmos DB | 自訂資料分割索引鍵路徑 | 固定 `id` | 
| MongoDB | 自訂共用金鑰  | 固定 `_id` | 
| 圖形 | 自訂資料分割索引鍵屬性 | 固定 `id` | 
| 資料表 | 固定 `PartitionKey` | 固定 `RowKey` | 

Azure Cosmos DB 使用雜湊型資料分割。 當您寫入項目時，Azure Cosmos DB 會將資料分割索引鍵值進行雜湊處理，然後使用雜湊的結果來判斷要在其中儲存項目的分割區。 Azure Cosmos DB 會將資料分割索引鍵相同的所有項目儲存在相同的實體分割區中。 選擇資料分割索引鍵是在設計階段必須進行的一項重要決策。 您必須選擇具有各種不同的值並且有平均存取模式的屬性名稱。 如果實體的資料分割到達它的儲存體限制相同的資料分割索引鍵的資料分割中的所有資料、 Azure Cosmos DB 傳回 「 資料分割索引鍵會達到 10 GB 的大小上限 」 的錯誤，且資料未分割，因此選擇 資料分割索引鍵是很匯入ant 決策。

> [!NOTE]
> 資料分割索引鍵最好有許多相異值 (至少數百至數千個)。
>

Azure DB Cosmos 容器可建立為*固定*或*無限制*在 Azure 入口網站。 固定大小的容器具有上限為 10 GB 和 10,000 RU/秒的輸送量。 若要建立為無限制的容器，您必須指定 1000 RU/秒的最小的輸送量，您必須指定資料分割索引鍵。

建議您檢查資料在分割區中分佈的方式。 若要在入口網站中進行此一檢查，請移至 Azure Cosmos DB 帳戶並按一下 [監視] 區段中的 [計量]，然後在右側窗格中按一下 [儲存體] 索引標籤，以查看資料在不同實體分割區中分割的方式。

![資源的資料分割](./media/partition-data/partitionkey-example.png)

左側影像顯示不良分割區索引鍵的結果，右側影像顯示良好分割區索引鍵的結果。 在左側影像中，您可以看到資料並未平均分佈於各個分割區中。 您應該盡量分散資料，讓圖表看起來類似於右側影像。

<a name="prerequisites"></a>
## <a name="prerequisites-for-partitioning"></a>資料分割的必要條件

實體資料分割來自動分割為**p1**和**p2**中所述[如何運作分割](#how-does-partitioning-work)，容器必須建立與 1000 RU/秒的輸送量或多個而且必須提供資料分割索引鍵。 在 Azure 入口網站中建立容器，選取**Unlimited**利用資料分割和自動調整的儲存容量選項。 

如果您在建立容器在 Azure 入口網站，或以程式設計方式並初始輸送量 1,000 RU/秒或以上，和您的資料包含資料分割索引鍵，您可以利用您的容器未變更資料分割-這包括**固定**大小容器，只要使用至少 1000 RU/秒 througput，在建立初始的容器和資料分割索引鍵存在於資料中。

如果您建立**固定**未資料分割索引鍵，或建立大小容器**固定**小於 1,000 RU/秒的輸送量的大小容器，容器無法自動分割這篇文章中所述。 若要將從容器像這樣的資料移轉到無限制的容器 （至少 1000 RU/秒的輸送量和資料分割索引鍵中有一個） 中，您需要使用[資料移轉工具](import-data.md)或[變更摘要文件庫](change-feed.md)至移轉所做的變更。 

## <a name="partitioning-and-provisioned-throughput"></a>資料分割與佈建的輸送量
Azure Cosmos DB 設計用來取得可預測的效能。 當您建立容器時，需以「每秒的[要求單位](request-units.md) (RU)」保留輸送量。 每項要求都會指派有與系統資源 (例如作業所使用的 CPU、記憶體和 IO) 數量成正比的 RU 費用。 讀取 1 KB 具有工作階段一致性的文件，會使用 1 RU。 不論儲存的項目數或同時執行的並行要求數，讀取一次都是 1 個 RU。 根據大小之不同，較大的項目需要較高的 RU。 如果您知道實體大小以及支援您應用程式所需的讀取次數，則可以佈建應用程式讀取需求確實需要的輸送量。 

> [!NOTE]
> 為達到容器的完整輸送量，您必須選擇資料分割索引鍵，讓您能將要求平均地分散到數個相異的資料分割索引鍵值。
> 
> 

<a name="designing-for-partitioning"></a>
## <a name="work-with-the-azure-cosmos-db-apis"></a>使用 Azure Cosmos DB API
您可以使用 Azure 入口網站或 Azure CLI 建立容器，並在任何時間進行調整。 本節說明如何建立容器，並在每個支援的 API 中指定輸送量和資料分割索引鍵定義。

### <a name="azure-cosmos-db-api"></a>Azure Cosmos DB API
下列範例示範如何使用 Azure Cosmos DB API 建立容器 (集合)。 

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

您可以使用 REST API 中的 `GET` 方法或使用其中一個 SDK 中的 `ReadDocumentAsync` 來讀取項目 (文件)。

```csharp
// Read document. Needs the partition key and the ID to be specified
DeviceReading document = await client.ReadDocumentAsync<DeviceReading>(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="mongodb-api"></a>MongoDB API
您可以使用 MongoDB API，透過您喜愛的工具、驅動程式或 SDK 建立分區化集合。 在此範例中，我們使用 Mongo 殼層建立集合。

在 Mongo 殼層中︰

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

若要建立資料表，使用 Azure Cosmos DB 資料表 API，請使用 CreateIfNotExists 方法。 

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

CloudTable table = tableClient.GetTableReference("people");
table.CreateIfNotExists(throughput: 800);
```

輸送量是設定為 CreateIfNotExists 的引數。

資料分割索引鍵會隱含地建立為 `PartitionKey` 值。 

您可以使用下列程式碼片段來擷取單一實體：

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
如需詳細資訊，請參閱[使用資料表 API 進行開發](tutorial-develop-table-dotnet.md)。

### <a name="graph-api"></a>圖形 API

使用圖形 API 時，必須使用 Azure 入口網站或 Azure CLI 建來立容器。 此外，因為 Azure Cosmos DB 是多重模型，您可以使用其中一種其他模型來建立及調整您的圖形容器。

您可以在 Gremlin 中使用資料分割索引鍵和識別碼來判讀任何頂點或邊緣。 例如，對於使用區域 (美國) 作為資料分割索引鍵和使用「西雅圖」作為資料列索引鍵的圖形，您可以使用下列語法找到頂點︰

```
g.V(['USA', 'Seattle'])
```

您可以使用資料分割索引鍵和資料列索引鍵來參考某個邊緣。

```
g.E(['USA', 'I5'])
```

如需詳細資訊，請參閱 [Azure Cosmos DB 的 Gremlin 支援](gremlin-support.md)。


<a name="designing-for-partitioning"></a>
## <a name="design-for-partitioning"></a>資料分割的設計
若要使用 Azure Cosmos DB 進行有效調整，您必須在建立容器時挑選適當的資料分割索引鍵。 選擇資料分割索引鍵時有兩個主要考量︰

* **查詢和交易的邊界**。 您選擇的分割區索引鍵應兼顧交易使用和將實體分散到多個分割區索引鍵 (以確保可調整的解決方案) 的需求。 以一個極端的情況來說，您可以針對所有項目設定相同的資料分割索引鍵，但這種做法可能會限制解決方案的延展性。 反過來，您可以為每個項目指派唯一的資料分割索引鍵。 這個做法具有高延展性，但是會讓您無法透過預存程序和觸發程序使用跨文件交易。 理想的資料分割索引鍵可讓您使用有效率的查詢，而且具有足夠的基數，可確保您的解決方案能加以調整。 
* **沒有儲存體和效能瓶頸**。 請務必選取允許寫入分散到不同相異值的屬性。 相同資料分割索引鍵的要求不能超過單一分割區的輸送量，因此會進行節流。 因此，請務必挑選不會在應用程式內導致「作用點」的資料分割索引鍵。 因為單一資料分割索引鍵的所有資料皆必須儲存在資料分割中，您應該在遇到有大量相同值的資料時，避免資料分割索引鍵。 

來看看一些真實案例和每個案例良好的資料分割索引鍵︰
* 如果您實作使用者設定檔後端，使用者識別碼是不錯的資料分割索引鍵選擇。
* 如果您在儲存 IoT 資料 (例如，裝置狀態)，裝置識別碼是不錯的資料分割索引鍵選擇。
* 如果您使用 Azure Cosmos DB 來記錄時間序列資料，主機名稱或處理序識別碼很適合作為資料分割索引鍵。
* 如果您有多組織用戶管理，租用戶識別碼是不錯的資料分割索引鍵選擇。

在一些使用案例 (例如 IoT 與使用者設定檔) 中，資料分割索引鍵可能與您的識別碼 (文件索引鍵) 相同。 在其他使用案例 (例如時間序列資料) 中，您的資料分割索引鍵可能與識別碼不同。

### <a name="partitioning-and-loggingtime-series-data"></a>資料分割和記錄/時間序列資料
Azure Cosmos DB 常見的其中一個使用案例是用在記錄與遙測。 您可能需要讀取/寫入大量資料，因此請務必挑選適當的資料分割索引鍵。 要做什麼選擇取決於讀取和寫入速率以及您預期要執行的查詢類型。 如何選擇適當資料分割索引鍵的一些秘訣如下：

* 如果您的使用案例牽涉到以較小的速率寫入已累積很長一段時間的資料，而且必須依時間戳記範圍和其他篩選器進行查詢，則使用彙總的時間戳記。 例如，以日期作為資料分割索引鍵是不錯的方法。 採取這個做法，您可以查詢單一資料分割中某一天的所有資料。 
* 如果您的寫入工作負載繁重 (這是更常見的情形)，請使用不是根據時間戳記的資料分割索引鍵。 採取這個做法，Azure Cosmos DB 可以將寫入工作平均分散到多個資料分割。 在這個案例中，主機名稱、處理序識別碼、活動識別碼或其他具有高基數的屬性是不錯的選擇。 
* 另一個做法是混合做法，採取此做法您會擁有多個容器，每天/每月各有一個容器，而且資料分割索引鍵是細微的屬性，例如主機名稱。 這個做法有優點，您可以根據時間範圍設定不同的輸送量。 例如，為本月份的容器佈建較高輸送量，因為它要讀取和寫入資料。 為前幾個月佈建較低的輸送量，因為它們只會讀取。

### <a name="partitioning-and-multitenancy"></a>資料分割與多組織用戶管理
如果您使用 Azure Cosmos DB 實作多組織用戶管理應用程式，有兩種常見的模式：一個租用戶一個資料分割索引鍵，和一個租用戶一個容器。 以下是每項方式的優缺點︰

* **一個租用戶一個資料分割索引鍵**。 在此模型中，租用戶共置於單一容器內。 但是，針對單一資料分割，可以執行單一租用戶內項目的查詢與插入。 您也可以跨租用戶內的所有項目實作交易邏輯。 因為多個租用戶共用一個容器，所以您可以節省儲存體和輸送量成本，方法是在單一容器內輪詢租用戶的資源，而不是為每個租用戶佈建額外的空餘空間。 缺點是無法隔離每個租用戶的效能。 整個容器的效能/輸送量增加與鎖定特定租用戶的增加。
* **一個租用戶一個容器**。 在此模型中，每個租用戶都有自己的容器，您可以保留每個租用戶的效能。 使用 Azure Cosmos DB 全新的佈建計價，這種模式對於具有少數租用戶的多重租用戶應用程式最具成本效益。

您也可以使用組合/分層的方式，來共置少數租用戶，並將較大的租用戶移轉到其專屬容器。

## <a name="next-steps"></a>後續步驟
在本文中，我們概述了使用任一 Azure Cosmos DB API 進行資料分割的概念和最佳做法。 

* 了解 [Azure Cosmos DB 中佈建的輸送量](request-units.md)。
* 了解 [Azure Cosmos DB 中的全域分散](distribute-data-globally.md)。



