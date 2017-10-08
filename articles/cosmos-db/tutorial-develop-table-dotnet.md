---
title: "Azure Cosmos DB: 開發以 hello 表格 API 在.NET |Microsoft 文件"
description: "深入了解如何使用適用於.NET 的 Azure Cosmos DB 的資料表 api toodevelop"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>開發以 hello 表格 API 在.NET 的 azure Cosmos DB:

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。

本教學課程涵蓋 hello 下列工作： 

> [!div class="checklist"] 
> * 建立 Azure Cosmos DB 帳戶 
> * 啟用在 hello app.config 檔案中的功能 
> * 建立資料表，使用 hello[表格 API](table-introduction.md) （預覽）
> * 加入實體 tooa 表 
> * 插入實體批次 
> * 擷取單一實體 
> * 使用自動次要索引來查詢實體 
> * 取代實體 
> * 刪除實體 
> * 刪除資料表
 
## <a name="tables-in-azure-cosmos-db"></a>Azure Cosmos DB 中的資料表 

Azure 的 Cosmos DB 會提供 hello[表格 API](table-introduction.md) （預覽） 的需要無結構描述設計的索引鍵-值存放區的應用程式。 [Azure 資料表儲存體](../storage/common/storage-introduction.md)Sdk 和 REST Api 可以使用以 Azure Cosmos DB toowork。 您可以使用 Azure Cosmos DB toocreate 資料表具有高輸送量需求。 Azure Cosmos DB 支援輸送量最佳化資料表 (非正式的名稱為「進階資料表」)，目前是公開預覽版。 

您可以繼續 toouse 資料表具有高的儲存體與較低的輸送量需求的 Azure 資料表儲存體。 Azure Cosmos DB 將介紹支援儲存體最佳化的資料表，在未來的更新中，與現有和新的 Azure 資料表儲存體帳戶會順暢地升級 tooAzure Cosmos DB。

如果您目前使用 Azure 資料表儲存體，您可以獲得下列的好處與 hello 「 高階資料表 」 預覽 hello:

- 具有多路連接及[自動和手動容錯移轉](regional-failover.md)的完備[全域散發](distribute-data-globally.md)
- 支援所有屬性 (次要索引) 之無從驗證結構描述的自動索引編製，以及快速查詢 
- 支援在任意數目的區域[獨立調整儲存體和輸送量](partition-data.md)
- 支援[專用的輸送量，每個資料表](request-units.md)，可以調整百 toomillions 每秒的要求
- 支援[五個可微調的一致性層級](consistency-levels.md)tootrade 關閉可用性、 延遲和一致性根據您的應用程式需求
- 在多個單一區域和能力 tooadd 99.99%可用性的高可用性、 區域和[領先業界全面 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db/)一般可用性
- 使用 hello 現有 Azure 儲存體.NET SDK 與任何程式碼變更 tooyour 應用程式

Hello 在預覽期間，Azure Cosmos DB 支援 hello 資料表使用 hello.NET SDK 的 API。 您可以下載 hello [Azure 儲存體預覽 SDK](https://aka.ms/premiumtablenuget) NuGet，從具有 hello 相同的類別和方法簽章為 hello [Azure 儲存體 SDK](https://www.nuget.org/packages/WindowsAzure.Storage)，但是也可以連接使用 hello tooAzure Cosmos DB 帳戶應用程式開發介面的資料表。

toolearn 進一步了解複雜的 Azure 資料表儲存體工作，請參閱：

* [簡介 tooAzure Cosmos DB： 表格 API](table-introduction.md)
* hello 有關可用的應用程式開發介面的完整詳細資料的資料表服務參考文件[.NET 參考的儲存體用戶端程式庫](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>關於本教學課程
本教學課程的開發人員熟悉 hello Azure 資料表儲存體 SDK，並希望 toouse hello premium 功能正在使用 Azure Cosmos DB。 它基礎[開始使用適用於.NET 的 Azure 資料表儲存體使用](table-storage-how-to-use-dotnet.md)，並示範如何 tootake 利用額外的功能讓次要索引，佈建的輸送量，多重主目錄。 我們將討論如何 toouse hello Azure 入口網站 toocreate Azure Cosmos DB 帳戶，然後建置並部署資料表的應用程式。 此外，也逐步解說 .NET 範例，這些範例可用來建立和刪除資料表，以及插入、更新、刪除和查詢資料表資料。 

如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

首先在 hello Azure 入口網站中建立 Azure Cosmos DB 帳戶。  

> [!TIP]
> * 已經有 Azure Cosmos DB 帳戶？ 如果是這樣，跳過[設定您的 Visual Studio 方案](#SetupVS)。
> * 您是否已有 Azure DocumentDB 帳戶？ 如果因此，您的帳戶現在是 Azure Cosmos DB 帳戶，而且您可以向前跳過[設定您的 Visual Studio 方案](#SetupVS)。  
> * 如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定您的 Visual Studio 方案](#SetupVS)。
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們來複製資料表中的應用程式 github 設定 hello 連接字串，並執行它。

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. 然後在 Visual Studio 中開啟 hello 方案檔。

## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。 您將使用在 hello 螢幕 toocopy hello 連接字串 hello 右邊 hello 複製按鈕到 hello 下一個步驟中的 hello app.config 檔案。

2. 在 Visual Studio 中，開啟 hello app.config 檔案。 

3. 從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello 帳戶鍵 app.config 中的值。使用先前建立的帳戶名稱在 app.config 中的 hello 帳戶名稱。
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse 標準 Azure 資料表儲存體與此應用程式，您需要 toochange hello 連接字串中的`app.config file`。 Azure 儲存體主索引鍵做為資料表帳戶名稱和金鑰使用 hello 帳戶名稱。 <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>建置和部署 hello 應用程式
1. 在 Visual Studio 中，以滑鼠右鍵按一下中的 hello 專案**方案總管 中**，然後按一下**管理 NuGet 封裝**。 

2. 在 hello NuGet**瀏覽**方塊中，輸入***WindowsAzure.Storage PremiumTable***。 請選取 [包括發行前版本]。

3. 從 hello 結果中，安裝 hello **WindowsAzure.Storage PremiumTable**選擇 hello 預覽版`0.0.1-preview`。 此動作會安裝 hello Azure 資料表儲存體封裝和所有相依性。

4. 按一下 CTRL + F5 toorun hello 應用程式。 

您現在可以返回 tooData 總管和看到查詢、 修改及使用此資料表的資料。 

> [!NOTE]
> 此應用程式與 Azure Cosmos DB 模擬器，您只需要 toochange hello 連接字串中的 toouse `app.config file`。 使用模擬器 hello 最大值。 <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Azure Cosmos DB 功能
Azure Cosmos DB 支援多種 hello Azure 資料表儲存體 API 中所沒有的功能。 hello 新功能可透過啟用 hello 下列`appSettings`組態值。 我們並未導入任何新簽章或多載 toohello 預覽 Azure 儲存體 SDK。 這可讓您 tooconnect tooboth standard 和 premium 資料表和工作和其他 Azure 儲存體服務，例如 Blob 和佇列。 


| Key | 說明 |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB 支援兩種連線模式。 在`Gateway`模式中，要求一律會 toohello Azure Cosmos DB 閘道，將它轉送 toohello 對應資料分割。 在`Direct`連線模式 hello 用戶端擷取的資料表 toopartitions hello 對應，並將要求直接針對資料分割。 我們建議`Direct`，hello 預設值。  |
| TableConnectionProtocol | Azure Cosmos DB 支援兩種連線通訊協定 - `Https` 和 `Tcp`。 `Tcp`是 hello 預設值，而且建議使用，因為它更精簡。 |
| TablePreferredLocations | 供讀取使用的慣用 (多路連接) 位置逗號分隔清單。 每個 Azure Cosmos DB 帳戶都可以與 1-30 個以上的區域建立關聯。 每個用戶端執行個體可以針對低度延遲讀取 hello 慣用順序指定這些區域的子集。 必須使用命名 hello 區及其[顯示名稱](https://msdn.microsoft.com/library/azure/gg441293.aspx)，例如`West US`。 另請參閱[多路連接 API](tutorial-global-distribution-table.md)。
| TableConsistencyLevel | 您可以在五個定義完善的一致性層級之間做選擇，以在延遲、一致性及可用性之間做取捨：`Strong`、`Session`、`Bounded-Staleness`、`ConsistentPrefix` 及 `Eventual`。 預設值為 `Session`。 hello 所選擇的一致性層級可讓多區域龐大的顯著的效能差異。 如需詳細資料，請參閱[一致性層級](consistency-levels.md)。 |
| TableThroughput | 表示每秒要求單位 (RU) 中的 hello 資料表所保留的輸送量。 單一資料表可支援每秒數億個 RU。 請參閱[要求單位](request-units.md)。 預設值為 `400` |
| TableIndexingPolicy | 對資料表內所有資料行進行一致且自動的次要索引編製 | JSON 字串合格 toohello 編製索引原則規格。 請參閱[編製索引原則](indexing-policies.md)toosee 如何變更檢索原則 tooinclude/排除特定資料行。 | 自動編製所有屬性 (字串的雜湊，以及數字的範圍) 的索引 |
| TableQueryMaxItemCount | 設定 hello 的每個資料表至單一反覆存取的查詢傳回的項目數上限。 預設值是`-1`，可讓 Azure Cosmos DB 以動態方式判斷 hello 值在執行階段。 |
| TableQueryEnableScan | 如果 hello 查詢無法使用 hello 索引的任何篩選，然後執行還是透過掃描。 預設值為 `false`。|
| TableQueryMaxDegreeOfParallelism | hello 執行跨資料分割查詢的平行處理原則程度。 `0`與任何預先提取，序列`1`序列與預先提取，且平行處理原則增加 hello 率較高的數值。 預設值是`-1`，可讓 Azure Cosmos DB 以動態方式判斷 hello 值在執行階段。 |

toochange hello 預設值，開啟 hello`app.config`從 Visual Studio 中的 [方案總管] 的檔案。 新增的 hello hello 內容`<appSettings>`如下所示的項目。 取代`account-name`hello 儲存體帳戶名稱和`account-key`與您的帳戶存取金鑰。 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello`Program.cs`檔案，並尋找這行程式碼建立 hello 表格資源。 

## <a name="create-hello-table-client"></a>建立 hello 資料表用戶端
您初始化`CloudTableClient`tooconnect toohello 資料表帳戶。

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
此用戶端使用 hello 初始化`TableConnectionMode`， `TableConnectionProtocol`， `TableConsistencyLevel`，和`TablePreferredLocations`組態值，如果 hello 應用程式設定中指定。
    
## <a name="create-a-table"></a>建立資料表
然後，您需使用 `CloudTable` 來建立資料表。 Azure Cosmos DB 中的資料表可以獨立擴充，以儲存體和輸送量、 和資料分割由自動 hello 服務。 Azure Cosmos DB 同時支援固定大小和無限制的資料表。 如需詳細資料，請參閱 [Azure Cosmos DB 中的資料分割](partition-data.md)。 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

在資料表的建立方式方面有重大的差異。 Azure Cosmos DB 會保留輸送量，而不像 Azure 儲存體針對交易是採用以耗用量為基礎的模型。 hello 保留模型具有兩個主要優點：

* 您的輸送量是專用/已保留的，因此當您的要求率正好在或低於所佈建的輸送量時，一律不會進行節流
* hello 保留模型較為[符合成本效益的輸送量為主的工作負載](key-value-store-cost.md)

您可以藉由設定 hello 設定來設定 hello 預設輸送量`TableThroughput`以每秒 RU （要求單位）。 

讀取 1 KB 實體會正規化為 1 RU 和其他作業都是正規化的 tooa 固定 RU 值根據其 CPU、 記憶體和 IOPS 的耗用量。 深入了解 [Azure Cosmos DB 中的要求單位](request-units.md)。

> [!NOTE]
> 當資料表儲存體 SDK 目前不支援修改的輸送量時，您可以立即使用隨時 hello Azure 入口網站或 Azure CLI 變更 hello 輸送量。

接著，我們會逐步解說 hello 簡單讀取及寫入使用 hello Azure 資料表儲存體 SDK (CRUD) 作業。 本教學課程會示範 Azure Cosmos DB 所提供之可預測的低個位數毫秒延遲和快速查詢。

## <a name="add-an-entity-tooa-table"></a>加入實體 tooa 表
Azure 資料表儲存體中的實體擴充 hello`TableEntity`類別，而且必須具有`PartitionKey`和`RowKey`屬性。 以下是一個客戶實體的範例定義。

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

下列程式碼片段的 hello 顯示實體與 tooinsert hello Azure 儲存體 SDK 的方式。 Azure Cosmos DB 可供任何規模的低延遲保證 hello 世界各地。

寫入完成 < 15 ms p99 在與大約是 6 ms p50 執行的應用程式在 hello 與 hello Azure Cosmos DB 帳戶相同的區域。 和這段期間寫入的 hello 事實的帳戶都已認可後 toohello 用戶端之後才它們會以同步方式進行複寫，內容經過永久認可之後，所有的內容會建立索引。

hello Azure Cosmos DB 資料表 API 為預覽狀態。 公開上市 hello p99 延遲保證備份 Sla，如其他 Azure Cosmos DB Api 的。 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>插入實體批次
Azure 資料表儲存體支援批次作業 API，可讓您結合更新、 刪除和插入 hello 相同的單一批次作業。 Azure Cosmos DB 沒有的某些 hello 限制 hello 批次 API 上作為 Azure 資料表儲存體。 例如，您可以執行多次讀取批次內，您可以執行多個寫入 toohello 內批次中的相同實體和每個批次的 100 個作業中沒有任何限制。 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>擷取單一實體
擷取 （取得），在 Cosmos Azure DB 中完成 < 10 毫秒在 p99 和 ~ 1 毫秒中 p50 在 hello 相同 Azure 區域。 您可以新增多區域 tooyour 帳戶針對低度延遲讀取，並藉由設定部署應用程式從其區域 （「 多路連接 」） 的 tooread `TablePreferredLocations`。 

您可以擷取單一實體，使用下列程式碼片段的 hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> 若要了解多路連接 API，請參閱[使用多個區域進行開發](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>使用自動次要索引來查詢實體
您可以使用 hello 查詢資料表`TableQuery`類別。 Azure Cosmos DB 具有寫入最佳化資料庫引擎，可自動為您資料表中的所有資料行編製索引。 在 Azure Cosmos DB 索引時，是無從驗證 tooschema。 因此，即使您的結構描述不同之間的資料列，或經過一段時間發展，hello 結構描述，它會自動索引。 由於 Azure Cosmos DB 支援自動次要索引，針對任何屬性的查詢可以使用 hello 索引，而且有效率地提供。

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

在預覽中，Azure Cosmos DB 支援 hello 同樣的查詢與 hello 表格 API 的 Azure 資料表儲存體的功能。 Azure Cosmos DB 也支援排序、彙總、地理空間查詢、階層及各種不同的內建函式。 在未來的服務更新中的 hello 資料表 API 中，將會提供 hello 額外的功能。 如需這些功能的概觀，請參閱 [Azure Cosmos DB 查詢](documentdb-sql-query.md)。 

## <a name="replace-an-entity"></a>取代實體
tooupdate 實體，擷取與 hello 表格服務，修改 hello 實體物件，然後再儲存 hello 變更變回 toohello 表格服務。 hello 下列程式碼變更現有的客戶電話號碼。 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
同樣地，您也可以執行 `InsertOrMerge` 或 `Merge` 作業。  

## <a name="delete-an-entity"></a>刪除實體
您已在使用 hello 擷取之後，您可以輕鬆地刪除實體的更新實體顯示的相同模式。 下列程式碼的 hello 擷取，並刪除一個 customer 實體。

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>刪除資料表
最後，下列程式碼範例的 hello 會從儲存體帳戶刪除資料表。 您可使用 Azure Cosmos DB 來立即刪除並重新建立資料表。

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>清除資源 

如果您不打算 toocontinue toouse 此應用程式，使用下列步驟 toodelete hello Azure 入口網站在此教學課程所建立的所有資源的 hello。   

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。  
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。 

## <a name="next-steps"></a>後續步驟

在本教學課程中，我們涵蓋 tooget 啟動 hello 表格 API 搭配使用 Azure Cosmos DB 的方式，您們 hello 下列： 

> [!div class="checklist"] 
> * 建立 Azure Cosmos DB 帳戶 
> * Hello app.config 檔案中啟用的功能 
> * 建立資料表 
> * 加入實體 tooa 表 
> * 插入一批實體 
> * 擷取單一實體 
> * 使用自動次要索引來查詢實體 
> * 取代實體 
> * 刪除實體 
> * 刪除資料表  

您現在可以繼續 toohello 下一個教學課程，並深入了解查詢資料表的資料。 

> [!div class="nextstepaction"]
> [查詢以 hello 表格 API](tutorial-query-table.md)
