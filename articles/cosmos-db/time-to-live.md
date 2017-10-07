---
title: "在 Azure Cosmos DB 時間 toolive aaaExpire 資料 |Microsoft 文件"
description: "Ttl，Microsoft Azure Cosmos DB 會提供自動清除從 hello 系統在一段時間之後的 hello 能力 toohave 文件。"
services: cosmos-db
documentationcenter: 
keywords: "toolive 時間"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>到期時間 toolive 使用自動 Azure Cosmos DB 集合中的資料
應用程式可以產生並儲存大量資料。 其中有些資料，例如電腦產生的事件資料、記錄檔和使用者工作階段資訊只能在有限的期間內使用。 一旦 hello 資料變得多餘 toohello hello 應用程式需要安全 toopurge 這項資料，並減少應用程式的 hello 儲存需求。

「 時間 toolive 」 或 TTL，Microsoft Azure Cosmos DB 會提供從 hello 資料庫中自動清除，在一段時間之後的 hello 能力 toohave 文件。 hello 預設時間 toolive 可以 hello 集合層級設定，並覆寫個別文件為基礎。 設定 TTL (不論是作為集合預設值或是在文件層級設定) 之後，Cosmos DB 就會自動移除自上次修改後存在時間達該指定時間 (以秒為單位) 的文件。

上次修改 hello 文件時，toolive Cosmos DB 中的時間就會使用針對位移。 toodo 此使用 hello`_ts`存在於每個文件的欄位。 hello _ts 欄位是 unix 樣式 epoch 時間戳記代表 hello 日期和時間。 hello`_ts`每次修改文件時，欄位會更新。 

## <a name="ttl-behavior"></a>TTL 行為
hello TTL 功能是由兩個層級-hello 集合層級和 hello 文件層級的 TTL 屬性控制。 hello 值會設定以秒為單位，而會被視為 delta 從 hello`_ts`在上次修改該 hello 文件。

1. DefaultTTL hello 集合
   
   * 如果遺失 （或 set toonull） 文件不會自動刪除。
   * 如果有的話，hello 值為"-1"= 無限 – 依預設不會過期的文件
   * 如果有的話，因此 hello 值是某個數字 ("n")-文件到期"n"秒之後在上次修改
2. TTL hello 文件： 
   
   * 屬性是 DefaultTTL 存在於 hello 父集合時，才適用。
   * 覆寫 hello 父集合的 hello DefaultTTL 值。

只要 hello 文件已過期 (`ttl`  +  `_ts` > = 目前的伺服器時間)，hello 文件標示為 「 過期 」。 將這些文件上允許任何操作，在此時間之後，將排除 hello 執行任何查詢結果。 hello 文件會實際刪除 hello 系統中，並視情況在稍後刪除 hello 背景。 這不會耗用任何[要求單位 (Ru)](request-units.md)從 hello 集合預算。

hello 遵循矩陣會顯示 hello 上方邏輯：

|  | DefaultTTL 遺漏/不 hello 集合上設定 | 集合上的 DefaultTTL = -1 | 集合上的 DefaultTTL = "n" |
| --- |:--- |:--- |:--- |
| 集合上遺漏 TTL |執行任何動作 toooverride 由於 hello 文件和集合有沒有 TTL 的概念文件層級。 |此集合中的所有文件都不會過期。 |在此集合中的 hello 文件將到期間隔 n 耗盡時。 |
| 文件上的 TTL = -1 |不在 hello 文件層級不會定義 hello 集合，因為 toooverride hello DefaultTTL 屬性可以覆寫文件。 文件上的 TTL 是 hello 系統未解譯的。 |此集合中的所有文件都不會過期。 |永遠不會過期 TTL = 1 這個集合中的 hello 文件。 所有其他文件將在 "n" 間隔之後過期。 |
| 文件上的 TTL = n |執行任何動作 toooverride hello 文件層級。 中的文件的 TTL hello 系統未解譯。 |hello 文件，ttl = n 試用期間隔 n，以秒為單位。 其他文件會繼承間隔 -1 且永遠不會過期。 |hello 文件，ttl = n 試用期間隔 n，以秒為單位。 其他文件會繼承 hello 集合"n"間隔。 |

## <a name="configuring-ttl"></a>設定 TTL
根據預設，時間 toolive 已停用根據預設，所有的 Cosmos DB 集合中，並在所有文件。

## <a name="enabling-ttl"></a>啟用 TTL
tooenable TTL 集合或集合中的 hello 文件上，您需要 tooset hello DefaultTTL 集合 tooeither-1 或屬性的非零的正數值。 設定 hello DefaultTTL 太-1 表示預設 hello 集合中的所有文件永遠會存留，但 hello Cosmos DB 服務應該監視的文件已覆寫此預設值，這個集合。

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>在集合上設定預設 TTL
您有可以 tooconfigure 預設時間 toolive 集合層級。 tooset hello TTL 集合，您需要 tooprovide 非零的正數值，指出 hello 期間 （秒），tooexpire hello 集合中的所有文件之後 hello 上次修改時間戳記的 hello 文件 (`_ts`)。 或者，您可以設定 hello 預設太-1，這表示預設 live 插入 toohello 集合中的所有文件會無限期。

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>在文件上設定 TTL
此外 toosetting 集合上的預設 TTL 您可以設定特定的 TTL 文件層級。 如此一來，將會覆寫 hello 預設值為 hello 集合。

* tooset hello TTL 文件中，您需要的 tooprovide 非零的正數值表示 hello 時間，以秒為單位，tooexpire hello 文件之後 hello 上次修改時間戳記的 hello 文件 (`_ts`)。
* 如果文件不有任何 [TTL] 欄位中，然後 hello hello 集合的預設會套用。
* Hello 集合層級，TTL 已停用，直到 TTL hello 集合上再次啟用為止，將會忽略 hello 文件上的 hello TTL 欄位。

以下是程式碼片段顯示如何 tooset hello TTL 到期，文件上：

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>在現有文件上延長 TTL
您可以執行 hello 文件上的任何寫入作業，以重設文件上的 hello TTL。 執行此動作將設定 hello `_ts` toohello 目前的時間，hello 倒數計時 toohello 文件及到期時，所設定的 hello `ttl`，再重新開始。 如果您想 toochange hello`ttl`的文件，您可以更新 hello 欄位一樣可以與任何其他可設定的欄位。

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>從文件移除 TTL
如果已設定的 TTL 文件上，您不再需要該文件 tooexpire，然後您可以擷取 hello 文件移除 hello TTL 欄位，取代 hello hello 伺服器上的文件。 當從 hello 文件移除 hello TTL 欄位時，將會套用 hello 預設值為 hello 集合。 toostop 文件不會過期，不會繼承 hello 集合則需要 tooset hello TTL 值太-1。

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>停用 TTL
toodisable TTL 完全在集合，然後停止 hello 背景處理從尋找 hello DefaultTTL hello 集合屬性應該刪除過期的文件。 刪除此屬性是不同於將它設定為太-1。 將新的文件設定太-1 表示新增 toohello 集合應永遠，但您可以在 hello 集合中特定文件上覆寫此。 Hello 集合中完全移除這個屬性表示的會到期的文件，即使已明確覆寫先前的預設值的文件。

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>常見問題集
**TTL 的費用為何？**

沒有任何額外的成本 toosetting 文件上的 TTL。

**多久需要 toodelete 我的文件後已啟動的 hello TTL？**

hello TTL 已啟動，且將無法再存取透過 CRUD 或查詢 Api 之後，立即過期 hello 文件。 

**文件上的 TTL 是否會對 RU 費用造成任何影響？**

否，在 Cosmos DB 中透過 TTL 刪除過期的文件將不會影響 RU 費用。

**沒有 hello TTL 功能僅適用於 tooentire 文件，或可以後到期的個別文件屬性的值？**

TTL 適用於 toohello 整份文件。 如果您想要 tooexpire 部分文件，則建議您從 hello tooa 個別的 「 連結 」 文件中的主要文件擷取 hello 部分，，然後使用該擷取的文件上的 TTL。

**Hello TTL 功能是否有任何特定索引的需求？**

是。 hello 集合必須有[編製索引原則集](indexing-policies.md)tooeither 一致或 Lazy。 嘗試 tooset DefaultTTL 集合具有索引組 tooNone 上的會發生錯誤時，將會嘗試 tooturn 關閉具有 DefaultTTL，已設定的集合上的索引。

## <a name="next-steps"></a>後續步驟
深入了解 Azure Cosmos DB toolearn 參考 toohello 服務[*文件*](https://azure.microsoft.com/documentation/services/cosmos-db/)頁面。

