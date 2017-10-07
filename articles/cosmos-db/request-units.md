---
title: "aaaRequest 單位 & 估計輸送量-Azure Cosmos DB |Microsoft 文件"
description: "深入了解 toounderstand，指定，並評估 Azure Cosmos DB 中的要求單位需求的方式。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Azure Cosmos DB 中的要求單位
現在可供使用︰Azure Cosmos DB [要求單位計算機 (英文)](https://www.documentdb.com/capacityplanner)。 深入了解 [預估您的輸送量需求](request-units.md#estimating-throughput-needs)。

![輸送量計算機][5]

## <a name="introduction"></a>簡介
[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是 Microsoft 的全域分散式多模型資料庫。 以 Azure Cosmos DB，您尚未 toorent 虛擬機器、 部署軟體，或監視資料庫。 Azure Cosmos DB 是操作，並持續受到 Microsoft 頂端工程師 toodeliver 世界類別可用性、 效能及資料保護。 您可以使用選擇的 API 來存取資料，因為 [DocumentDB SQL](documentdb-sql-query.md) (文件)、MongoDB (文件)、[Azure 資料表儲存體](https://azure.microsoft.com/services/storage/tables/) (索引鍵值) 和 [Gremlin (英文)](https://tinkerpop.apache.org/gremlin.html) (圖表) 皆受到原 生支援。 hello 貨幣的 Azure Cosmos DB 為 hello 要求單位 (RU)。 RUs，與您不需要 tooreserve 讀/寫容量或佈建 CPU、 記憶體和 IOPS。

Azure Cosmos DB 支援的 Api 以不同的作業，範圍從簡單的讀取和寫入 toocomplex graph 查詢。 由於並非所有要求都都相同，就都會指派正規化的數量**要求單位**根據計算需要的 tooserve hello 要求 hello 金額。 作業的要求單位的 hello 數目是具決定性，而且您可以追蹤 hello Azure Cosmos DB 中透過回應標頭的任何作業所使用的要求單位數目。 

tooprovide 可預測的效能，您需要 tooreserve 輸送量單位的 100 RU/秒。 

閱讀這篇文章之後, 您將會無法 tooanswer hello 下列問題：  

* 什麼是要求單位和要求費用？
* 如何指定集合的要求單位容量？
* 如何估計應用程式的要求單位需求？
* 如果超過集合的要求單位容量，會發生什麼事？

如同 Azure Cosmos DB 多模型資料庫，所以我們將會針對應用程式開發介面文件、 圖形/節點 graph API 的資料表/實體資料表應用程式開發介面參考 tooa 集合文件的重要 toonote。 輸送量這份文件，我們將一般化 toohello 概念容器/項目。

## <a name="request-units-and-request-charges"></a>要求單位和要求費用
Azure Cosmos DB 都會提供快速、 可預測的效能，由*保留*資源 toosatisfy 應用程式的輸送量需求。  應用程式會載入並存取一段時間的模式變更，因為 Azure Cosmos DB 可讓您 tooeasily 增加，或減少 hello 保留的輸送量可用 tooyour 應用程式的數量。

有了 Azure Cosmos DB，保留的輸送量是根據每秒處理的要求單位來指定。 您可以視為要求單位的輸送量貨幣，讓您*保留*數量保證的要求單位可用 tooyour 每秒為基礎的應用程式。  Azure Cosmos DB 中的每個作業 (寫入文件、執行查詢、更新文件) 都會耗用 CPU、記憶體和 IOPS。  也就是說，每個作業都會產生「要求費用」，這是以「要求單位」來表示。  了解 hello 因素會影響要求單位的費用，您的應用程式輸送量需求，以及可讓您 toorun 成本儘可能有效的應用程式。 hello 查詢總管也是查詢的完美工具 tootest hello 核心。

我們建議您藉由監看下列影片，其中 Aravind Ramachandran 說明要求單位，以及可預測的效能與 Azure Cosmos DB hello 開始使用。

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>在 Azure Cosmos DB 中指定要求單位容量
當啟動新的集合、 資料表或圖表時，您會指定 hello 號碼的要求單位 (RU 每秒) 秒您想保留。 根據 hello 佈建輸送量，Azure Cosmos DB 配置實體分割區 toohost 您的集合，並分割/rebalances 資料在資料分割的成長。

Azure Cosmos DB 需要資料分割索引鍵的 toobe 指定集合已佈建以供 2,500 要求單位或更高版本時。 資料分割索引鍵也是必要的 tooscale 集合的輸送量超過 2,500 在 hello 未來的要求單位。 因此，強烈建議 tooconfigure[資料分割索引鍵](partition-data.md)時建立的容器，不論您初始的輸送量。 因為您的資料可能會有 toobe 分成多個資料分割，就會需要 toopick 具有高基數 (相異值的 100 toomillions)，讓您收集/資料表/圖形與要求可以縮放統一 Azure Cosmos db 的資料分割索引鍵。 

> [!NOTE]
> 資料分割索引鍵是一種邏輯界限，而不是實體界限。 因此，您不需要 toolimit hello 數目相異的資料分割索引鍵值。 它實際上是較佳 toohave 比較明顯分割區較少的索引鍵值，因為 Azure Cosmos DB 具有多個負載平衡選項。

以下是用來建立集合與 3000 的程式碼片段要求每個第二個使用單位 hello.NET SDK:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure Cosmos DB 會在輸送量的保留模型上運作。 也就是，您需要付費 hello 段輸送量*保留*，不論有多少的輸送量主動*用*。 為您的應用程式負載、 資料和使用模式變更您可以輕鬆地向上和向下調整 hello 保留 RUs 透過 Sdk 的數量，或使用 hello [Azure 入口網站](https://portal.azure.com)。

對應每個集合/資料表/圖形 tooan `Offer` Azure Cosmos DB 已 hello 佈建輸送量的相關中繼資料中的資源。 您可以變更配置的 hello 輸送量查閱 hello 對應優惠資源容器，然後更新以 hello 新的處理量值。 以下是變更集合 too5 hello 輸送量的程式碼片段，每個第二個使用 000 要求單位 hello.NET SDK:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

當您變更 hello 輸送量時沒有任何影響 toohello 可用性，您的容器。 通常 hello 新增保留的輸送量 hello 新產能的應用程式上的數秒內是有效。

## <a name="request-unit-considerations"></a>要求單位的考量
評估 hello Azure Cosmos DB 容器的要求單位 tooreserve 數目時，重要 tootake hello 考量下列變數：

* **項目大小**。 大小會增加 hello 使用的單位 tooread 或寫入 hello 資料也會增加。
* **項目屬性計數**。 假設預設索引的所有屬性，hello 使用的單位 toowrite 文件/節點/ntity hello 屬性計數增加時，會增加。
* **資料一致性**。 使用強式或繫結失效的資料一致性層級，額外的單位會取用的 tooread 項目。
* **已編製索引的屬性**。 每個容器上的索引原則會判定預設要編製哪些索引的屬性。 藉由限制 hello 索引的屬性數目，或藉由啟用延遲索引，您可以減少您的要求單位耗用量。
* **編製文件索引**。 根據預設，每個項目會自動編製索引，您會耗用較少的要求單位，如果您選擇不 tooindex 部分的項目。
* **查詢模式**。 查詢的 hello 複雜性會影響作業耗用多少要求單位。 述詞的 hello 數目、 性質 hello 述詞、 投射、 Udf、 數目和 hello 大小會影響所有的 hello 成本 hello 來源資料集的查詢作業。
* **指令碼使用方式**。  如同查詢、 預存程序和觸發程序會耗用根據 hello 複雜度 hello 作業正在執行的要求單位。 當您開發應用程式時，檢查 hello 要求電量標頭 toobetter 了解如何每一項作業會耗用要求單位容量。

## <a name="estimating-throughput-needs"></a>估計輸送量需求
要求單位是要求處理成本的標準化量值。 單一要求單位代表 hello 處理所需的容量 tooread （透過自我連結或識別碼） （不含系統屬性） 的 10 個唯一的屬性值的項目所組成的單一 1 KB。 要求 toocreate （插入），取代或刪除相同項目會耗用更多的處理從 hello 服務的 hello，藉此多個要求單位。   

> [!NOTE]
> 1 的要求單位的 hello 基準為 1 KB 項目對應 tooa 簡單取得自我連結或 hello 項目的識別碼。
> 
> 

例如，以下是資料表，其中顯示多少要求單位 tooprovision 在三個不同的項目大小 （1 KB、 4 KB 和 64 KB） 和兩個不同的效能層級 （每秒 500 讀取 + 100 寫入/秒與 500 讀取/秒 + 500 寫入/秒）。 在工作階段，設定 hello 資料的一致性，且 tooNone hello 檢索原則設定。

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>項目大小</strong></p></td>
            <td valign="top"><p><strong>讀取/秒</strong></p></td>
            <td valign="top"><p><strong>寫入/秒</strong></p></td>
            <td valign="top"><p><strong>要求單位</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1,000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3,000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1.3) + (100 * 7) = 1,350 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1.3) + (500 * 7) = 4,150 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9,800 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29,000 RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>使用 [小算盤] 的要求單位 hello
正常 toohelp 客戶調整其處理能力數量的估計值，所以在 web 架構[要求單位計算機](https://www.documentdb.com/capacityplanner)toohelp 估計 hello 要求單位需求一般作業，包括：

* 項目建立 (寫入)
* 項目讀取
* 項目刪除
* 項目更新

hello 工具也包含支援估計 hello 您提供的範例項目為基礎的資料存放區需求。

使用 hello 工具很簡單：

1. 上傳一或多個具代表性的項目。
   
    ![上傳項目 toohello 要求單位計算機][2]
2. tooestimate 資料儲存需求，請輸入 hello 總數的項目中，您預期 toostore。
3. 輸入 hello 數目的項目建立、 讀取、 更新和刪除的作業，您需要 （每秒為單位）。 tooestimate hello 要求單位費用的項目更新作業上, 傳一份 hello 從上方步驟 1 包含一般的欄位更新的範例項目。  例如，如果項目更新通常修改名為 lastLogin 和 userVisits，兩個屬性，則只需複製 hello 範例項目，更新這兩個屬性，以 hello 值，並上傳 hello 複製項目。
   
    ![在 hello 要求單位計算機輸入輸送量需求][3]
4. 按一下計算，並檢查 hello 結果。
   
    ![要求單位計算機結果][4]

> [!NOTE]
> 如果您有會大幅不同索引屬性的大小和 hello 數項目類型，然後上傳的每個範例*類型*典型的項目 toohello 的工具，然後再計算 hello 結果。
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>使用 hello Azure Cosmos DB 要求電量回應標頭
每個回應 hello Azure Cosmos DB 服務從包含自訂標頭 (`x-ms-request-charge`)，其中包含使用 hello 要求的 hello 要求單位。 也可透過 hello Azure Cosmos DB Sdk 存取此標頭。 在 hello.NET SDK，RequestCharge 是 hello ResourceResponse 物件的屬性。  查詢，hello Azure 入口網站中的 hello Azure Cosmos DB 查詢總管會提供執行查詢的要求計量資訊。

![檢查在 hello 查詢總管 RU 費用][1]

這一點，估計 hello 保留輸送量應用程式所需數量的方法之一是 toorecord hello 要求單位電量與執行一般作業，針對您的應用程式所使用的代表項目相關聯，然後您預期執行每秒估計 hello 作業數目。  能確定 toomeasure，而且包含一般的查詢和 Azure Cosmos DB 指令碼使用。

> [!NOTE]
> 如果您有會大幅不同索引屬性的大小和 hello 數項目類型，然後記錄每個相關聯的 hello 適用的作業要求單位收費*類型*的典型的項目。
> 
> 

例如：

1. 記錄 hello 要求單位收費 （插入） 所建立的一般項目。 
2. 典型的項目中讀取的要求單位費用記錄 hello。
3. 資料錄 hello 要求單位的更新的一般項目費用。
4. 一般、 常見的項目查詢的要求單位費用記錄 hello。
5. 記錄 hello 要求單位收費用的任何自訂指令碼 （預存程序、 觸發程序、 使用者定義函數） 透過 hello 應用程式
6. 計算 hello 需要給定作業的 hello 估計數的單位您預期 toorun 每秒的要求。

### <a id="GetLastRequestStatistics"></a>使用 API for MongoDB 的 GetLastRequestStatistics 命令
MongoDB 的 API 支援自訂的命令， *getLastRequestStatistics*，擷取指定作業的 hello 要求需付費。

比方說，在 hello Mongo 殼層，執行您要 tooverify hello 要求不需要支付費用的 hello 作業。
```
> db.sample.find()
```

接下來，執行 hello 命令*getLastRequestStatistics*。
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

這一點，估計 hello 保留輸送量應用程式所需數量的方法之一是 toorecord hello 要求單位電量與執行一般作業，針對您的應用程式所使用的代表項目相關聯，然後您預期執行每秒估計 hello 作業數目。

> [!NOTE]
> 如果您有會大幅不同索引屬性的大小和 hello 數項目類型，然後記錄每個相關聯的 hello 適用的作業要求單位收費*類型*的典型的項目。
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>使用 API for MongoDB 的入口網站計量
hello MongoDB 資料庫是 toouse hello 要求單位的良好的估計費用您 api 的最簡單方式 tooget [Azure 入口網站](https://portal.azure.com)度量。 以 hello*的要求數目*和*要求電量*圖表，您可以取得每個作業的要求單位數量的估計，耗用和要求單位的數量它們會耗用相對 tooone 另一個。

![API for MongoDB 入口網站計量][6]

## <a name="a-request-unit-estimation-example"></a>要求單位估計範例
請考慮下列 ~ 1 KB 文件的 hello:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> 文件會在 Azure Cosmos DB，縮短，因此 hello 系統計算上述 hello 文件的大小為略小於 1 KB。
> 
> 

hello 下表顯示大約要求此項目上的一般作業的單位收費 (hello 近似的要求單位收費假設 hello 帳戶一致性層級設定得 「 工作階段 」 和所有項目會自動編製索引):

| 作業 | 要求單位費用 |
| --- | --- |
| 建立項目 |~15 RU |
| 讀取項目 |~1 RU |
| 依識別碼查詢項目 |~2.5 RU |

此外下, 表顯示概略的要求單位費用 hello 應用程式中使用的典型查詢：

| 查詢 | 要求單位費用 | # 個傳回的項目 |
| --- | --- | --- |
| 依識別碼選取食物 |~2.5 RU |1 |
| 依製造商選取食物 |~7 RU |7 |
| 依食物群組選取並依重量排序 |~70 RU |100 |
| 選取食物群組中的前 10 個食物 |~10 RU |10 |

> [!NOTE]
> RU 費用會根據 hello 傳回項目數目而有所不同。
> 
> 

利用此資訊，我們可以估計 hello RU 需求的作業和我們預期每秒查詢這個應用程式指定 hello 號碼：

| 作業/查詢 | 每秒估計的數目 | 必要的 RU 數 |
| --- | --- | --- |
| 建立項目 |10 |150 |
| 讀取項目 |100 |100 |
| 依製造商選取食物 |25 |175 |
| 依食物群組選取 |10 |700 |
| 選取前 10 個 |15 |總共 150 個 |

在此情況下，我們預期平均輸送量需求為 1,275 RU/秒。  四捨五入為最接近 100 toohello，我們會佈建 1300 RU/秒針對此應用程式的集合。

## <a id="RequestRateTooLarge"></a> 超過 Azure Cosmos DB 中保留的輸送量限制
前文提過要求單位耗用量會評估為每秒的速率，是否是空的 hello 預算。 超過 hello 的應用程式的佈建的要求單位容器中，要求速率 toothat 集合將會受到節流，直到 hello 速率低於 hello 保留層級。 Hello RequestRateTooLargeException （HTTP 狀態碼 429） 要求，並傳回 hello x ms-重試-之後-ms 標頭指出 hello 一段時間，以毫秒為單位，hello 使用者之前，必須等候，節流發生時，會先結束 hello 伺服器本項 hello 要求。

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

如果您打算 hello.NET 用戶端 SDK 和 LINQ 查詢，大部分的 hello 您永遠不會有 toodeal 與這個例外狀況，如 hello 目前版本的.NET 用戶端 SDK hello 隱含攔截這個回應的時間，方面 hello 伺服器指定 retry-after 標頭，並重試 hello 要求。 除非正在多個用戶端同時存取您的帳戶，將會成功 hello 下次重試。

如果您有多個用戶端累積運作 hello 要求率超過 hello 預設重試行為可能不敷使用，並 hello 用戶端將會擲回狀態碼 429 toohello 應用程式與 DocumentClientException。 在這類情況下，您可以考慮處理重試行和您的應用程式錯誤處理常式，或增加 hello 保留的輸送量 hello 容器中的邏輯。

## <a id="RequestRateTooLargeAPIforMongoDB"></a> 超過 API for MongoDB 中保留的輸送量限制
超過集合的佈建的 hello 要求單位的應用程式將會受到節流，直到 hello 速率低於 hello 保留層級。 Hello 後端節流發生時，會先結束 hello 要求*16500*錯誤碼-*太多要求*。 根據預設，應用程式開發介面 for MongoDB。 將自動重試 too10 時間傳回前*太多要求*錯誤碼。 如果您收到許多*太多要求*錯誤代碼，您可以考慮在您的應用程式錯誤處理常式中任一加入重試行或[提高 hello 集合hello保留的輸送量](set-throughput.md).

## <a name="next-steps"></a>後續步驟
深入了解 Azure Cosmos DB 資料庫使用保留輸送量 toolearn 瀏覽這些資源：

* [Azure Cosmos DB 定價](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [在 Azure Cosmos DB 中分割資料](partition-data.md)

toolearn 深入了解 Azure Cosmos DB，請參閱 hello Azure Cosmos DB[文件](https://azure.microsoft.com/documentation/services/cosmos-db/)。 

tooget 入門規模和效能測試以 Azure Cosmos DB，請參閱[效能與延展測試 Azure Cosmos db](performance-testing.md)。

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
