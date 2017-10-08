---
title: "Azure CosmosDB︰每分鐘的要求單位 (RU/m) | Microsoft Docs"
description: "了解如何藉由使用 tooreduce 成本要求每分鐘的單位。"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Azure Cosmos DB 之每分鐘的要求單位

Azure 的 Cosmos DB 是設計的 toohelp 您得到快速、 可預測的效能和順暢地連同您的應用程式成長的小數位數。 您可以根據每秒和每分鐘 (RU/m) 的細微度，在 Cosmos DB 容器上佈建輸送量。 hello 每分鐘的資料粒度的佈建的輸送量為使用的 toomanage hello 工作負載發生在每秒的資料粒度的非預期的激增。 

本文章提供 hello 佈建每分鐘 (RU/m) 的要求單位的運作方式的概觀。 請注意，佈建 RU/m 的 hello 目標是 tooprovide 周圍預期需求 （特別是如果您需要 toorun 分析操作的資料之上） 和 spiky 工作負載的效能預測性。 我們想要的 toohave 我們的客戶使用他們佈建，使快速調整與安心詳細 hello 輸送量。

閱讀這篇文章之後, 您將無法 tooanswer hello 下列問題：

* 每分鐘的要求單位如何運作？
* Hello 要求單位每分鐘和秒的要求單位之間的差異為何？
* 如何 tooprovision RU/m 嗎？
* 在哪種情況下應該考慮佈建每分鐘的要求單位？
* 如何 toouse hello 入口網站的度量 toooptimize，我的成本和效能？
* 定義哪一種要求可能會耗用 RU/m 預算？

## <a name="provisioning-request-units-per-minute-rum"></a>佈建每分鐘的要求單位 (RU/m)

時您提供 Azure Cosmos DB 在 hello 第二個資料粒度 （RU/秒），您會收到 hello 保證您的要求成功在低延遲，如果您的輸送量尚未超過 hello 該秒內佈建的容量。 RU/m hello 資料粒度是在與您的要求會在該分鐘內成功的 hello 保證 hello 分鐘。 比較 toobursting 系統中，我們會先確認您所取得的 hello 效能可預測，而您可以規劃。

每分鐘的佈建運作方式的 hello 方式很簡單：

* 每小時及新增 tooRU/s 計費 RU/m。 如需詳細資訊，請瀏覽 Azure Cosmos DB [價格頁面](https://aka.ms/acdbpricing)。
* 您可以在集合等級啟用 RU/m。 即可透過 hello Sdk （Node.js、 Java 或.Net） 或透過 hello 入口網站 （也包括 MongoDB API 工作負載）
* 當啟用 RU/m 時，針對每個 100 RU/秒佈建，您也可以取得 1000 RU/m 佈建 （hello 比率會是 10 倍）
* 在某一秒內，只有當您在該秒內已超過您的每秒佈建時，要求單位才會取用您的 RU/m 佈建
* 一次 hello 60 秒的期間內 (UTC) 結束，要每分鐘的佈建的 hello
* 只有對每個資料分割最多佈建 5,000 RU/s 的集合，才能啟用 RU/m。 如果您調整輸送量需求，而且每個資料分割達到如此高的佈建等級，您會收到警告訊息

以下是具體的範例，其中客戶可以佈建 10kRU/s 和 100kRU/m，在佈建 10,000 RU/s 和 100,000 RU/m 的集合上，90 秒期間的尖峰佈建 (50kRU/秒) 可節省 73% 的成本：

* 第 1 個第二個： hello RU/m 預算設定 100000
* 第 3 秒： 要求單位的耗用量已 11,010 RUs、 1,010 RUs 上方 hello RU/秒佈建期間，第二個 hello。 因此，1,010 RUs 被扣除 hello RU/m 預算。 98,990 RUs 可供 hello hello RU/m 預算的下一個 57 秒數
* 第 29 秒： 期間的第二個大型高峰發生 (> 高於佈建每秒 4 x) 的要求單位的 hello 耗用量，46,920 俄文。 36,920 RUs 被扣除 92,323 RUs （28 秒） too55，403 RUs （第 29 秒） 從卸除的 hello RU/m 預算
* 61st 第二個： RU/m 預算設回 too100，000 俄文。
 
![圖形顯示 hello 耗用量，以及佈建 Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>使用 RU/m 指定要求單位容量

建立 Azure Cosmos DB 集合時，您會指定 hello 號碼的要求單位 (RU 每秒) 秒您想保留 hello 集合。 您也可以決定是否要讓 tooadd RU 每分鐘。 這可以透過 hello 入口網站或 hello SDK。 

### <a name="through-hello-portal"></a>透過 hello 入口網站

佈建集合時只需要按一下，即可啟用或停用每分鐘的 RU。 

 ![螢幕擷取畫面顯示如何在 Azure 入口網站 hello tooset RU/m](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>透過 hello SDK
首先，這是重要 toonote RU/m 」 僅適用於下列 Sdk hello:

* .Net 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

以下是用來建立集合與每分鐘使用 hello.NET SDK 的第二個和 30000 要求單位每 3000 的要求單位的程式碼片段：

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

以下是變更集合 too5 hello 輸送量的程式碼片段，000 要求每秒單位數不會每分鐘使用佈建 RU hello.NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>適合案例

在本節中，我們提供一些案例的概觀，這些案例適合啟用每分鐘的要求單位。

**開發/測試環境：**適合。 在 hello 開發階段中，如果您要測試您的應用程式使用不同的工作負載，RU/m 可提供 hello 彈性在這個階段。 Hello 時[模擬器](local-emulator.md)是很好的免費工具 tootest Azure Cosmos DB。 不過如果您想 toostart 雲端環境中的，您將會有很大的彈性與 RU/m 臨機操作效能需求。 您會有更多時間進行開發，不必一開始就擔心效能需求。 我們建議您從 hello 最小 RU/秒佈建並啟用 RU/m。

**無法預測、尖峰、每分鐘細微度的需求︰**適合 – 節省︰25-75%。 我們看到 RU/m 提供明顯的改善，且大部分的實際執行案例都屬於這一類。 如果您有幾次在一分鐘中具有特殊圖文集 IoT 工作負載執行的查詢時系統發出大量插入 hello 相同 time、 spiky 處理需求，您將需要額外容量。 建議您套用以下的逐步方法，將您的資源需求最佳化。

 ![此圖表顯示 5 分鐘細微度的要求耗用量](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *圖 - RU 耗用量基準測試*

**安心使用︰**適合 – 節省︰10-20%。 有時候，您只想 toohave 安心，而不必擔心潛在尖峰流量和節流。 這個功能會為您的 hello 右移一個。 在此情況下，我們建議啟用 RU/m，並稍微降低每秒佈建。 當您將不會嘗試 toooptimize 積極您佈建，此情況下與不同 hello 上方。 這比較傾向於「零節流」的心態。

重要的作業，以臨機操作的需求： 我們有時建議 tooonly 讓重要的作業存取 RU/m 預算，因此不會發生 hello 預算取用臨機操作或較不重要的作業。 可以輕鬆地定義於 hello 一節。

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>使用 hello 入口網站的度量 toooptimize 成本和效能

**在未來幾週 hello，我們將進一步開發監視您的輸送需求之俄文分鐘耗用量 toooptimize hello 內容。**

透過 hello 入口網站的度量，您可以看到您使用與 RU 規則 RU 秒中有多少分鐘。 監視這些計量應該可以協助您將佈建最佳化。 

我們建議您如何以逐步方法 toouse RU/m tooyour 優點。 針對每個步驟中，您應該代表您的工作負載 （它可能是小時、 天，或甚至數週） 的完整循環的 hello RU 耗用量的概觀及深入 hello 善用您佈建。

這種方式背後的 hello 原則是的 toomake 做為您提供的輸送量可能 tooa 佈建符合您的下列效能條件的點為關閉。 

![此圖表顯示 5 分鐘細微度的要求耗用量](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello 最佳佈建點為您的工作負載，您需要 toounderstand:

* 取用模式︰沒有、不頻繁或持續性的尖峰？ 小 (平均 2 倍)、中、大 (平均大於 10 倍) 尖峰？
* 節流要求的百分比︰您是否覺得稍微節流也沒有關係？ 如果是的話，多少才適合？ 

一旦您已識別您的目標是什麼，您將無法 tooget 接近 toohello 最佳佈建。

tooassist，我們想 tooprovide toooptimize 您佈建方式根據 RU/m 耗用整體的指引。 本指南不會套用 tooall 種類的工作負載，但 hello 私人預覽中的知識為基礎。 我們可能隨著更多經驗而變更這些基準︰

|RU/m % 使用率|RU/m 的使用程度|建議的佈建動作|
|---|---|---|
|0-1%|使用率不足|降低 RU/秒 tooconsume 詳細 RU/m|
|1-10%|使用情況良好|持續 hello 相同佈建層級嗎|
|10% 以上|過度使用|增加 RU/秒 toorely 較少的 RU/m|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>選取的作業可能會耗用 hello RU/m 預算

在要求層級，您可以也啟用/停用 RU/m 預算 tooserve hello 要求無論作業類型。 如果規則的佈建的 Ru/秒預算一經 hello 要求無法取用 hello RU/m 預算，此要求會被調整。 根據預設，如果啟動 RU/m 輸送量預算，則由 RU/m 預算支應任何要求。 

以下是用來停用 RU/m 預算 CRUD 和查詢作業使用 hello DocumentDB API 的程式碼片段。

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>後續步驟

在本文中，我們已描述了 Azure Cosmos DB 中的資料分割運作方式、如何建立分割集合，以及如何為您的應用程式挑選適當的資料分割索引鍵。

* 使用 Azure Cosmos DB 執行規模和效能測試。 如需範例，請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)。
* 開始撰寫程式碼以 hello [Sdk](documentdb-sdk-dotnet.md)或 hello [REST API](/rest/api/documentdb/)。
* 了解 Azure Cosmos DB 中[佈建的輸送量](request-units.md) 

