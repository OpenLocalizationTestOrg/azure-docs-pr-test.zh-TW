---
title: "aaaPerformance 提示-Azure Cosmos DB NoSQL |Microsoft 文件"
description: "了解用戶端設定選項 tooimprove Azure Cosmos DB 資料庫效能"
keywords: "如何 tooimprove 資料庫效能"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Azure Cosmos DB 的效能秘訣
Azure Cosmos DB 是一個既快速又彈性的分散式資料庫，可在獲得延遲與輸送量保證的情況下順暢地調整。 您沒有可以 toomake 主要架構變更，或撰寫複雜的程式碼 tooscale 以 Cosmos DB 資料庫。 相應增加和減少就像進行單一 API 呼叫或 [SDK 方法呼叫](set-throughput.md#set-throughput-sdk)一樣簡單。 不過，因為 Cosmos DB 透過網路呼叫有是您可以進行 tooachieve 尖峰效能的用戶端最佳化。

如果您詢問「如何改善我的資料庫效能？ 請考慮下列選項的 hello:

## <a name="networking"></a>網路
<a id="direct-connection"></a>

1. **原則︰使用直接連接模式**

    用戶端會 tooCosmos DB 的連線效能，特別是針對觀察到的用戶端延遲有很重要的影響。 有兩個索引鍵的組態設定可用來設定用戶端連線原則 – hello 連接*模式*和 hello[連接*通訊協定*](#connection-protocol)。  hello 兩個可用的模式如下：

   1. 閘道模式 (預設值)
   2. 直接模式

      閘道模式支援所有 SDK 平台上，而且是 hello 設定預設值。  如果嚴格防火牆限制在公司網路中執行您的應用程式，閘道模式會是 hello 最好的選擇，因為它使用標準 HTTPS 連接埠 hello 和單一的端點。 hello 效能權衡取捨，不過，每次讀取或寫入 tooCosmos DB 的資料閘道模式牽涉到額外的網路躍點。 因為這個緣故，直接模式提供更佳的效能，因為 toofewer 網路躍點。
<a id="use-tcp"></a>
2. **連線原則： 使用 hello TCP 通訊協定**

    使用直接模式時，有兩個可用的通訊協定選項：

   * TCP
   * HTTPS

     Cosmos DB 提供透過 HTTPS 的簡單且開放 RESTful 程式設計模型。 此外，它會提供有效率的 TCP 通訊協定，其在其通訊模型中也是 RESTful，而且可透過 hello.NET 用戶端 SDK。 直接 TCP 和 HTTPS 皆使用 SSL 來進行初始驗證和加密流量。 為了達到最佳效能，使用 hello TCP 通訊協定時可能。

     TCP 連接埠 443 TCP 在使用閘道模式時，為 hello Cosmos DB 的連接埠，且 10255 hello MongoDB 應用程式開發介面連接埠。 在直接存取模式，在加法 toohello 閘道的連接埠，使用 TCP 時要 tooensure hello 連接埠 10000 和 20000 之間的範圍是開啟的因為 Cosmos DB 會使用動態 TCP 連接埠。 如果這些連接埠未開啟，而且您嘗試 toouse TCP，您會收到 503 服務無法使用錯誤。

     hello 連線模式設定 hello 建構 hello DocumentClient hello ConnectionPolicy 參數執行個體的期間。 如果使用直接模式時，也可以設定 hello 通訊協定在 hello ConnectionPolicy 參數內。

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    因為 TCP 中才支援直接存取模式，如果使用閘道模式，然後 hello HTTPS 通訊協定一律用於以 hello 閘道 toocommunicate 和 hello 通訊協定值 hello ConnectionPolicy 會被忽略。

    ![圖中的 hello Azure Cosmos DB 的連線原則](./media/performance-tips/connection-policy.png)

3. **第一次要求呼叫 OpenAsync tooavoid 啟動延遲**

    根據預設，hello 第一個要求會具有較高的延遲，因為它有 toofetch hello 位址路由表。 這個 hello 上的啟動延遲第一次要求時，您應該一次在初始化期間呼叫 OpenAsync() tooavoid。

        await client.OpenAsync();
   <a id="same-region"></a>
4. **為了效能在相同 Azure 區域中共置用戶端**

    當呼叫 Cosmos DB 中的任何應用程式 hello 與相同區域的位置，可能 hello Cosmos DB 資料庫。 大約的比較，則會呼叫的 hello 1-2 毫秒但 hello 西部之間的 hello 是美國東部 coast hello 延遲時間內完成，相同區域內的 DB tooCosmos > 50 毫秒。 根據從 hello 用戶端 toohello Azure 資料中心的界限傳遞，hello 要求所花費的 hello 路由要求 toorequest 可能變更這樣的延遲。 hello 最低可能延遲達成方式是確保 hello 電話應用程式是位於 hello 與 hello 相同的 Azure 區域佈建 Cosmos DB 端點。 如需可用區域的清單，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services)。

    ![圖中的 hello Azure Cosmos DB 的連線原則](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **增加執行緒/工作數目**

    因為呼叫 tooAzure Cosmos DB 都是透過 hello 網路，您可能需要 toovary hello 程度的平行處理原則，您的要求，以便 hello 用戶端應用程式也需要花費很少要求之間等候的時間。 例如，如果您使用。網路的[工作平行程式庫](https://msdn.microsoft.com//library/dd460717.aspx)，hello 100 的讀取或寫入 tooCosmos DB 的工作順序中建立。

## <a name="sdk-usage"></a>SDK 的使用方式
1. **安裝 hello 最新的 SDK**

    hello Cosmos DB Sdk 不斷在提升的 tooprovide hello 達到最佳效能。 請參閱 hello [Cosmos DB SDK](documentdb-sdk-dotnet.md)頁面 toodetermine hello 最新的 SDK，並檢閱增強功能。
2. **使用單一 Cosmos DB 用戶端 hello 存留期的應用程式**

    請注意，每個 DocumentClient 執行個體都具備執行緒安全，並且在直接模式中運作時執行有效率的連接管理和位址快取。 tooallow 有效率的連接管理 DocumentClient 更佳的效能，而它時，建議 hello hello 應用程式存留期 toouse DocumentClient appdomain 的單一執行個體。

   <a id="max-connection"></a>
3. **增加使用閘道模式時每部主機的 System.Net MaxConnections**

    使用閘道模式時，都是透過 HTTPS/REST cosmos DB 要求，並會受到 toohello 預設連線限制每個主機名稱或 IP 位址。 您可能需要 tooset hello MaxConnections tooa 較高的值 (100-1000)，讓 hello 用戶端程式庫可以利用多個同時連線 tooCosmos DB。 在 hello.NET SDK 1.8.0 和以上版本，hello 預設值為[ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)為 50 和 toochange hello 值，您可以設定 hello [Documents.Client.ConnectionPolicy.MaxConnectionLimit](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa 較高的值。   
4. **微調分割之集合的平行查詢**

     DocumentDB.NET SDK 版本 1.9.0 和上方支援平行查詢，可讓您 tooquery 分割的集合，以平行方式 (請參閱[使用 hello Sdk](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks)和相關的 hello[程式碼範例](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs)的詳細的資訊）。 平行查詢是設計的 tooimprove 查詢延遲和輸送量透過其序列的對應項目。 平行查詢提供兩個參數的使用者可以微調 toocustom 調整其的需求 （a) MaxDegreeOfParallelism: toocontrol hello 最大的資料分割數目然後可查詢以平行方式，以及 （b) MaxBufferedItemCount: toocontrol hello 數目預先擷取的結果。

    (a) ***微調 MaxDegreeOfParallelism\:*** 平行查詢的運作方式是以平行方式查詢多個分割。 不過，與尊重 toohello 查詢時方向循序擷取個別的資料分割收集的資料。 因此，設定 hello MaxDegreeOfParallelism toohello 資料分割數目必須 hello 最大的機會達到 hello 大部分的高效能查詢中，提供所有其他的系統條件維持 hello 相同。 如果您不知道的資料分割的 hello 數目，您可以設定 hello MaxDegreeOfParallelism tooa 數量太多，，和 hello MaxDegreeOfParallelism hello 系統選擇 hello 最小值 （資料分割，提供使用者輸入的數字）。

    如果 hello 資料分佈的所有資料分割方面 toohello 查詢與平行查詢產生 hello 最佳優點的重要 toonote 它。 如果 hello 分割集合被分割方式的所有或大多數的查詢所傳回的 hello 資料集中於幾個資料分割 （一個資料分割最壞情況下），則 hello hello 查詢效能瓶頸會因為這些資料分割。

    （b)***微調 MaxBufferedItemCount\: ***平行查詢時，設計的 toopre 提取結果 hello 用戶端正在處理目前的批次 hello 的結果。 hello 預先擷取查詢的整體延遲改善的協助。 MaxBufferedItemCount 是 hello 參數 toolimit hello 預先擷取的結果數目。 設定 MaxBufferedItemCount toohello 必須是數字傳回結果 （或更高的數字） 可讓從預先擷取的 hello 查詢 tooreceive 最大效益。

    請注意，預先提取 works hello 相同方式不論 hello MaxDegreeOfParallelism，沒有單一緩衝區 hello 資料來自所有分割區。  
5. **開啟伺服器端 GC**

    在某些情況下可能有助於減少 hello 的記憶體回收的頻率。 在.NET 中，設定[gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue。
6. **在 RetryAfter 間隔實作降速**

    在進行效能測試期間，您應該增加負載，直到系統對小部分要求進行節流處理為止。 如果節流處理，hello 用戶端應用程式應該在節流閥 hello 指定伺服器的輪詢重試間隔。 尊重 hello 輪詢可確保您花最少的重試之間的時間等候。 重試原則支援是內含的和更新版本 1.8.0 的 hello DocumentDB [.NET](documentdb-sdk-dotnet.md)和[Java](documentdb-sdk-java.md)，1.9.0 版本和更新版本的 hello [Node.js](documentdb-sdk-node.md)和[Python](documentdb-sdk-python.md)，並支援所有版本的 hello [.NET Core](documentdb-sdk-dotnet-core.md) Sdk。 如需詳細資訊，請參閱[超過保留的輸送量限制](request-units.md#RequestRateTooLarge)和 [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx)。
7. **相應放大用戶端工作負載**

    如果您要測試高輸送量層級 (> 50000 RU/秒)，hello 用戶端應用程式可能會因為 toohello 機器須出上 CPU 或網路使用率的 hello 瓶頸。 如果達到這個點之後，您可以繼續 toopush hello Cosmos DB 帳戶進一步透過向外延展您的用戶端應用程式，在多部伺服器。
8. **快取較低讀取延遲的文件 URI**

    快取文件 Uri 儘可能為 hello 最佳讀取效能。
   <a id="tune-page-size"></a>
9. **微調查詢/讀取摘要，以提升效能的 hello 頁面大小**

    執行大量讀取時使用讀取摘要功能 (例如，ReadDocumentFeedAsync) 的文件，或發出 DocumentDB SQL 查詢時，會傳回 hello 結果以分割方式如果 hello 結果集太大。 根據預設，會以 100 個項目或 1 MB 的區塊傳回結果 (以先達到的限制為準)。

    tooreduce hello 數目的網路所需的往返 tooretrieve 所有適用的結果，您可以增加使用 x-ms-最大的項目-計數要求標頭 tooup too1000 hello 頁面大小。 在您需要的情況 toodisplay 的幾個結果，比方說，如果您的使用者介面或應用程式 API 傳回 10 個結果的時間，您也可以減少 hello 頁面大小 too10 tooreduce hello 輸送量所耗用的讀取和查詢。

    您也可以設定 hello 頁面大小使用 hello 可用 Cosmos DB Sdk。  例如：

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **增加執行緒/工作數目**

    請參閱[執行緒/工作的數目增加](#increase-threads)hello 網路功能 區段中。

11. **使用 64 位元主機處理序**

    當您使用 DocumentDB.NET SDK 版本 1.11.4 和更高版本，hello DocumentDB SDK 適用於 32 位元主控件程序中。 不過，若使用跨分割區查詢，建議您使用 64 位元主機處理以獲得改進的效能。 下列類型的應用程式的 hello 有 32 位元主控件做為 hello 預設值處理，因此在順序 toochange 亦 too64 位元，請遵循這些步驟會依據您的應用程式的 hello 類型：

    - 可執行的應用程式，這可藉由來取消選取 hello**建議使用 32 位元**選項在 hello**專案屬性**視窗的 hello**建置** 索引標籤。

    - VSTest 以基礎的測試專案，這可藉由選取**測試**->**測試設定**->**預設為 X64 的處理器架構**，從 hello **Visual Studio 測試**功能表選項。

    - 提供在本機部署的 ASP.NET Web 應用程式，作法是藉由檢查 hello**使用 hello 64 位元版本的 IIS Express 用於網站和專案**下**工具**-> **選項**->**專案和方案**->**Web 專案**。

    - 對於部署在 Azure 上的 ASP.NET Web 應用程式，即可啟用此選擇 hello**平台為 64 位元**在 hello**應用程式設定**hello Azure 入口網站上。

## <a name="indexing-policy"></a>索引原則
1. **使用延遲索引加快尖峰時間擷取速率**

    Cosmos DB 可讓您 toospecify – 在 hello 集合層級 – 編製索引的原則，可讓您 toochoose 如果您想在自動編製索引，或不集合 toobe hello 文件。  此外，您也可以選擇同步 (一致) 和非同步 (延遲) 索引更新。 根據預設，hello 索引會以同步方式在每個插入、 取代或刪除文件 toohello 集合中的更新。 同步模式可讓 hello 查詢 toohonor hello 相同[一致性層級](consistency-levels.md)hello 的文件會讀取沒有任何延遲 hello 索引太"趕上"。

    延遲索引可能會被視為的案例資料以暴增，而您想 tooamortize hello 所需 tooindex 內容在較長的一段時間。 延遲索引也可讓您 toouse 您有效地佈建輸送量和服務在尖峰時間寫入要求，延遲最少。 重要 toonote，不過，啟用延遲索引時，查詢結果的最終一致不管 hello 一致性層級為 hello Cosmos DB 帳戶設定它。

    因此，（IndexingPolicy.IndexingMode 設定 tooConsistent） 一致的檢索模式會產生 hello 最高的要求單位收費每次寫入，Lazy （IndexingPolicy.IndexingMode 設定 tooLazy） 模式，沒有索引編製索引時 （IndexingPolicy.Automatic 設定tooFalse) 的寫入 hello 次有零個索引的成本。
2. **從索引編製中排除未使用的路徑以加快寫入速度**

    Cosmos DB 的編製索引原則也可讓您的文件路徑 tooinclude 或排除的索引編製索引的路徑 （IndexingPolicy.IncludedPaths 和 IndexingPolicy.ExcludedPaths） 利用 toospecify。 索引路徑的 hello 使用可以提供改進的寫入效能與較低的索引儲存體案例中的 hello 查詢模式事先知道，因為索引的成本直接的相互關聯 toohello 編製索引的唯一路徑的數目。  例如，下列程式碼的 hello 顯示如何 tooexclude hello 的整個區段文件 （也稱為 子樹狀目錄中） 從索引使用 hello"*"萬用字元。

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    如需詳細資訊，請參閱 [Azure Cosmos DB 索引編製原則](indexing-policies.md)。

## <a name="throughput"></a>輸送量
<a id="measure-rus"></a>

1. **測量和調整較低的要求單位/秒使用量**

    Cosmos DB 會提供一組豐富的資料庫作業，包括關聯式及階層式查詢 Udf、 預存程序與觸發程序-所有作業的資料庫集合中的 hello 文件。 這些作業的每個相關聯的 hello 成本會根據 hello CPU、 IO 和記憶體所需 toocomplete hello 作業而異。 而不是思考並管理硬體資源，您可以視為要求單位 (RU) 的單一量值為 hello 資源需要 tooperform 各種資料庫作業和服務應用程式的要求。

    [要求單位](request-units.md)會根據您所購買的容量單位的 hello 數目每個資料庫帳戶佈建。 要求單位消耗量是以每秒的速率來計算。 應用程式超過 hello 佈建的要求單位率的 hello 速率低於 hello 保留層級 hello 帳戶前，會限制他們的帳戶。 如果應用程式需要較高層級的輸送量，您可以另外購買容量單位。

    查詢的 hello 複雜性會影響作業耗用多少要求單位。 述詞的 hello 數目、 性質 hello 述詞，Udf、 數目和 hello 大小會影響所有的 hello 成本 hello 來源資料集的查詢作業。

    toomeasure hello 負擔任何作業 （建立、 更新或刪除），檢查 hello x ms-要求免費標頭 (或 hello ResourceResponse 中的對等 RequestCharge 屬性<T>或 FeedResponse<T> hello.NET SDK 中) toomeasurehello 這些作業所使用的要求單位數目。

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    hello 要求傳回此標頭的費用是您佈建輸送量的分數 (亦即，2000 Ru / 秒)。 例如，如果 hello 上述查詢會傳回 1000年 1 KB 文件，hello 操作的 hello 成本為 1000年。 因此，每秒內 hello 伺服器會接受調整後續要求之前只有兩個這類要求。 如需詳細資訊，請參閱[要求單位](request-units.md)和 hello[要求單位計算機](https://www.documentdb.com/capacityplanner)。
<a id="429"></a>
2. **處理速率限制/要求速率太大**

    當用戶端嘗試 tooexceed hello 保留的輸送量的帳戶時，沒有任何效能降低的 hello 伺服器並會使用超過 hello 保留層級的輸送量容量。 hello RequestRateTooLarge （HTTP 狀態碼 429） 要求，並傳回 hello x ms-重試-之後-ms 標頭指出 hello 一段時間，以毫秒為單位，hello 使用者必須等候本項 hello 要求，將會先結束 hello 伺服器。

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    hello Sdk 全都隱含攔截這個回應，尊重 hello 伺服器指定 retry-after 標頭，然後重試 hello 要求。 除非正在多個用戶端同時存取您的帳戶，將會成功 hello 下次重試。

    如果您有多個用戶端 hello 要求速率高於累積一致的方式運作，hello 預設重試的計數目前組 too9 內部由 hello 用戶端可能不敷使用;在此情況下，hello 用戶端會擲回 DocumentClientException 與狀態碼 429 toohello 應用程式。 可以變更 hello ConnectionPolicy 執行個體上設定 hello RetryOptions hello 預設重試次數。 根據預設，hello DocumentClientException 429 顯示狀態碼會傳回累計等候時間為 30 秒後，如果 hello 要求會繼續 toooperate 上方 hello 要求率。 發生這種情況即使當 hello 目前的重試計數小於 hello 最大重試計數，不管 hello 預設值是 9 或使用者定義的值。

    雖然 hello 自動化重試行為有助於 tooimprove 恢復功能和可用性的 hello 大部分的應用程式，它可能會在 odds 進行效能評定基準，特別當測量延遲時。  hello 用戶端觀察到的延遲會超過如果 hello 實驗點擊 hello 伺服器節流閥，會導致 hello 用戶端 SDK toosilently 重試。 tooavoid 延遲尖峰效能實驗期間每個作業所傳回的量值 hello 電量，並確定要求正在低於 hello 保留的要求的速率。 如需詳細資訊，請參閱 [要求單位](request-units.md)。
3. **輸送量較高之少量文件的設計**

    hello 給定作業的要求費用 （也就是要求處理成本） 是直接相互關聯 toohello hello 文件大小。 大型文件的作業成本高於小型文件的作業成本。

## <a name="next-steps"></a>後續步驟
範例應用程式使用 tooevaluate Cosmos DB 幾個用戶端電腦上的高效能案例，請參閱[效能和延展性測試以 Cosmos DB](performance-testing.md)。

此外，請參閱更多關於設計您的應用程式規模和高效能、 toolearn[資料分割和 Azure Cosmos DB 中的縮放比例](partition-data.md)。
